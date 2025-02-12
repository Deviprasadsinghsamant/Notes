
# **B. BLoC (Business Logic Component)**

BLoC is an advanced state management solution using **streams** to separate business logic from the UI.

### **Key Features**

- **Strict separation of UI and logic**.
- **Uses Streams (Sink & Stream)** for state updates.
- **Good for large-scale apps**.

### **Example: Counter App using BLoC**

**Step 1: Install BLoC** Add to `pubspec.yaml`:

```yaml
dependencies:
  flutter_bloc: ^8.1.0
```

**Step 2: Create a Counter BLoC**

```dart
import 'package:flutter_bloc/flutter_bloc.dart';

// Events for CounterBloc
abstract class CounterEvent {}
class IncrementEvent extends CounterEvent {}

// Bloc to handle counter logic
class CounterBloc extends Bloc<CounterEvent, int> {
  CounterBloc() : super(0) {
    on<IncrementEvent>((event, emit) => emit(state + 1));
  }
}
```

**Step 3: Using the BLoC in UI**

```dart
import 'package:flutter/material.dart';
import 'package:flutter_bloc/flutter_bloc.dart';
import 'counter_bloc.dart'; // Import the BLoC file

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: BlocProvider(
        create: (context) => CounterBloc(),
        child: CounterScreen(),
      ),
    );
  }
}

class CounterScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("BLoC Counter")),
      body: Center(
        child: BlocBuilder<CounterBloc, int>(
          builder: (context, count) {
            return Text("Counter: $count", style: TextStyle(fontSize: 24));
          },
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () => context.read<CounterBloc>().add(IncrementEvent()),
        child: Icon(Icons.add),
      ),
    );
  }
}
```

### **How It Works**

1. `CounterBloc` listens for `IncrementEvent` and updates the counter state.
2. `BlocProvider` provides the BLoC instance.
3. `BlocBuilder` listens for state changes and updates the UI.

✅ **Best For:** Large-scale apps that require structured architecture.
