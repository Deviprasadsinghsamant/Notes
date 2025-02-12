



# **A. Riverpod (State Management Without `context`)**

Riverpod is an improved version of Provider that eliminates the need for `BuildContext`, making state management more flexible and testable.

### **Key Features**

- **No need for `BuildContext`** → Makes accessing state simpler.
- **Performance Optimized** → Only rebuilds necessary parts of the UI.
- **Uses `StateNotifier`** → More structured approach to managing state.

### **Example: Counter App using Riverpod**

**Step 1: Install Riverpod** Add the following dependency in `pubspec.yaml`:

```yaml
dependencies:
  flutter_riverpod: ^2.0.0
```

**Step 2: Create a Provider for State Management**

```dart
import 'package:flutter_riverpod/flutter_riverpod.dart';

// Defining a StateNotifier to manage the counter's state
class CounterNotifier extends StateNotifier<int> {
  CounterNotifier() : super(0);

  void increment() => state++;
}

// Defining a provider for the CounterNotifier
final counterProvider = StateNotifierProvider<CounterNotifier, int>((ref) {
  return CounterNotifier();
});
```

**Step 3: Using the Provider in UI**

```dart
import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';
import 'counter_provider.dart'; // Import the provider file

void main() {
  runApp(ProviderScope(child: MyApp())); // Wrap the app with ProviderScope
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: CounterScreen(),
    );
  }
}

class CounterScreen extends ConsumerWidget {
  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final counter = ref.watch(counterProvider); // Watching the provider

    return Scaffold(
      appBar: AppBar(title: Text("Riverpod Counter")),
      body: Center(child: Text("Counter: $counter", style: TextStyle(fontSize: 24))),
      floatingActionButton: FloatingActionButton(
        onPressed: () => ref.read(counterProvider.notifier).increment(),
        child: Icon(Icons.add),
      ),
    );
  }
}
```

### **How It Works**

1. `StateNotifierProvider` manages the state.
2. `ConsumerWidget` watches the provider and updates UI.
3. `ref.read(counterProvider.notifier).increment()` updates state.

✅ **Best For:** Scalable apps where `Provider` would be too complex.

---




