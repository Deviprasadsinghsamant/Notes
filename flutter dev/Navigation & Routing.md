# **Navigation & Routing in Flutter** 🚀

Navigation in Flutter allows users to move between different screens (pages) in an app. There are multiple ways to handle routing, and understanding **Named vs. Anonymous Routing**, **Navigator 1.0 vs Navigator 2.0**, **Passing Arguments**, and **Page Transitions & Animations** is crucial.

---

## **1. Named vs. Anonymous Routing**

Flutter provides **two ways** to navigate between screens:

- **Anonymous Routing** → Uses `Navigator.push()` with `MaterialPageRoute`.
- **Named Routing** → Uses `Navigator.pushNamed()` with a predefined route map.

### **🔹 Anonymous Routing (Basic Navigation)**

This is the simplest way to navigate between screens. It **directly creates a new screen instance** when needed.

**Example: Navigating using `Navigator.push()`**

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    home: FirstScreen(),
  ));
}

class FirstScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("First Screen")),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            // Navigate to SecondScreen using push()
            Navigator.push(
              context,
              MaterialPageRoute(builder: (context) => SecondScreen()),
            );
          },
          child: Text("Go to Second Screen"),
        ),
      ),
    );
  }
}

class SecondScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Second Screen")),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            // Go back to the previous screen
            Navigator.pop(context);
          },
          child: Text("Go Back"),
        ),
      ),
    );
  }
}
```

### **🔹 Named Routing (Centralized Route Management)**

Named routing allows **centralized route management**, making navigation more structured.

**Step 1: Define Routes in `MaterialApp`**

```dart
void main() {
  runApp(MaterialApp(
    initialRoute: '/',
    routes: {
      '/': (context) => FirstScreen(),
      '/second': (context) => SecondScreen(),
    },
  ));
}
```

**Step 2: Navigate Using Named Routes**

```dart
class FirstScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("First Screen")),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            // Navigate to SecondScreen using named route
            Navigator.pushNamed(context, '/second');
          },
          child: Text("Go to Second Screen"),
        ),
      ),
    );
  }
}
```

✅ **Best for:** Medium to large applications where navigation is centralized.

---

## **2. Navigator 1.0 vs Navigator 2.0**

Flutter introduced **Navigator 2.0** to handle **complex navigation**, such as **deep linking and back-stack manipulation**.

### **🔹 Navigator 1.0 (Imperative Navigation)**

The traditional way of navigation (as seen above) is **imperative**, meaning **each screen push/pop is controlled manually**.

### **🔹 Navigator 2.0 (Declarative Navigation)**

Navigator 2.0 uses a **declarative API**, making it suitable for **deep linking** and **URL-based navigation**.

✅ **When to use Navigator 2.0?**

- When you need **deep linking** (open a specific screen using a URL).
- When you need **custom route management** (back-stack manipulation).

**Basic Example of Navigator 2.0**

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp.router(
      routerDelegate: MyRouterDelegate(),
      routeInformationParser: MyRouteInformationParser(),
    );
  }
}

// Custom Router Delegate
class MyRouterDelegate extends RouterDelegate with ChangeNotifier, PopNavigatorRouterDelegateMixin {
  final GlobalKey<NavigatorState> navigatorKey = GlobalKey<NavigatorState>();
  List<String> _pages = ["/"];

  @override
  Widget build(BuildContext context) {
    return Navigator(
      key: navigatorKey,
      pages: [
        MaterialPage(child: FirstScreen(), key: ValueKey("FirstScreen")),
        if (_pages.contains("/second"))
          MaterialPage(child: SecondScreen(), key: ValueKey("SecondScreen")),
      ],
      onPopPage: (route, result) {
        if (!route.didPop(result)) {
          return false;
        }
        _pages.removeLast();
        notifyListeners();
        return true;
      },
    );
  }

  void push(String route) {
    _pages.add(route);
    notifyListeners();
  }
}

// Example Screens
class FirstScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("First Screen")),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            (Router.of(context).routerDelegate as MyRouterDelegate).push("/second");
          },
          child: Text("Go to Second Screen"),
        ),
      ),
    );
  }
}

class SecondScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Second Screen")),
      body: Center(child: Text("Welcome to Second Screen!")),
    );
  }
}
```

✅ **Best for:** Apps requiring **deep linking, web navigation, or complex stateful navigation**.

---

## **3. Passing Arguments Between Screens**

Sometimes, you need to pass **data between screens**.

### **🔹 Anonymous Route with Arguments**

```dart
// Navigate with arguments
Navigator.push(
  context,
  MaterialPageRoute(
    builder: (context) => SecondScreen(data: "Hello!"),
  ),
);

// Receiving arguments in SecondScreen
class SecondScreen extends StatelessWidget {
  final String data;
  SecondScreen({required this.data});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(child: Text(data)),
    );
  }
}
```

### **🔹 Named Route with Arguments**

```dart
// Passing arguments
Navigator.pushNamed(
  context,
  '/second',
  arguments: 'Hello from First Screen',
);

// Receiving arguments
class SecondScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final String data = ModalRoute.of(context)!.settings.arguments as String;
    return Scaffold(
      body: Center(child: Text(data)),
    );
  }
}
```

✅ **Best for:** Sending user-specific data (IDs, names, etc.).

---

## **4. Page Transitions & Animations**

Flutter allows **custom transitions** between pages.

### **🔹 Default Page Transition**

```dart
Navigator.push(
  context,
  PageRouteBuilder(
    pageBuilder: (context, animation, secondaryAnimation) => SecondScreen(),
    transitionsBuilder: (context, animation, secondaryAnimation, child) {
      return FadeTransition(
        opacity: animation,
        child: child,
      );
    },
  ),
);
```

### **🔹 Custom Slide Transition**

```dart
Navigator.push(
  context,
  PageRouteBuilder(
    pageBuilder: (context, animation, secondaryAnimation) => SecondScreen(),
    transitionsBuilder: (context, animation, secondaryAnimation, child) {
      return SlideTransition(
        position: Tween<Offset>(
          begin: Offset(1, 0), // Start from right
          end: Offset.zero,
        ).animate(animation),
        child: child,
      );
    },
  ),
);
```

✅ **Best for:** Making UI transitions smooth and engaging.

---

# **Layman’s Explanation 🏗️**

1. **Navigator is like a stack of books** 📚.
    
    - When you push a new screen (`Navigator.push()`), it's like adding a book on top.
    - When you pop a screen (`Navigator.pop()`), it's like removing the top book.
2. **Named routes are like a Table of Contents** 📖.
    
    - Instead of opening books manually, you can jump to a specific page using a name.
3. **Navigator 2.0 is like a web browser** 🌍.
    
    - It tracks history, supports deep links, and can manage complex navigation.

---

# **Final Thoughts**

- Use **Anonymous Routing** for **simple apps**.
- Use **Named Routing** for **medium/large apps**.
- Use **Navigator 2.0** for **web apps & complex navigation**.
- Use **Page Transitions** to **improve UI experience**.

Would you like more in-depth examples? 😊🚀