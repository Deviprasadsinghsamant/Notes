# **D. MobX**

MobX is based on **observable state management** using **reactions**.

### **Key Features**

- **Uses Observables, Actions, and Reactions**.
- **Automatic UI updates when observables change**.

### **Example: Counter App using MobX**

**Step 1: Install MobX**

```yaml
dependencies:
  flutter_mobx: ^2.0.6+5
  mobx: ^2.2.0
dev_dependencies:
  build_runner: ^2.1.11
  mobx_codegen: ^2.1.1
```

**Step 2: Create a Counter Store**

```dart
import 'package:mobx/mobx.dart';

part 'counter_store.g.dart';

class CounterStore = _CounterStore with _$CounterStore;

abstract class _CounterStore with Store {
  @observable
  int count = 0;

  @action
  void increment() {
    count++;
  }
}
```

Run `flutter pub run build_runner build` to generate `counter_store.g.dart`.

**Step 3: Using MobX in UI**

```dart
import 'package:flutter/material.dart';
import 'package:flutter_mobx/flutter_mobx.dart';
import 'counter_store.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  final CounterStore counterStore = CounterStore();

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text("MobX Counter")),
        body: Center(
          child: Observer(
            builder: (_) => Text("Counter: ${counterStore.count}", style: TextStyle(fontSize: 24)),
          ),
        ),
        floatingActionButton: FloatingActionButton(
          onPressed: counterStore.increment,
          child: Icon(Icons.add),
        ),
      ),
    );
  }
}
```

✅ **Best For:** Complex apps needing **reactive programming**.

Would you like further details on any specific approach? 🚀