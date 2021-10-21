# Vainas de flutter


## Async call using FutureBuilder when pressing a button
Insert this widget into a widget or whatever.

Just remember to call the foking `setState()` method
```dart

// Esta vaina contiene el futureBuilder
class MyFutureStatefulWidget extends StatefulWidget {
  const MyFutureStatefulWidget({ Key? key }) : super(key: key);

  @override
  _MyFutureStatefulWidgetState createState() => _MyFutureStatefulWidgetState();
}

class _MyFutureStatefulWidgetState extends State<MyFutureStatefulWidget> {

  Future<String>? _result;

  Future<String> computate(){
    return Future<String>.delayed(
      const Duration(seconds: 1),
      () => 'Data Loaded!!!',
    );
  }

  void asignar(){
      setState(() {
        _result = computate();
      });
  }

  @override
  Widget build(BuildContext context) {
    return FutureBuilder<String>(
      future: _result,
      builder: (BuildContext context, AsyncSnapshot<String> snapshot) {
        List<Widget> children;

        if(snapshot.hasData){
          children = <Widget>[
              const Icon(
                Icons.check_circle_outline,
                color: Colors.green,
                size: 60,
              ),
              Padding(
                padding: const EdgeInsets.only(top: 16),
                child: Text('Result: ${snapshot.data}'),
              )
          ];

        }else if (snapshot.hasError){
          children = <Widget>[
              const Icon(
                Icons.error_outline,
                color: Colors.red,
                size: 60,
              ),
              Padding(
                padding: const EdgeInsets.only(top: 16),
                child: Text('Error: ${snapshot.error}'),
              )
          ];

        }else{
          children =  <Widget>[
              const SizedBox(
                child: CircularProgressIndicator(),
                width: 60,
                height: 60,
              ),
              const Padding(
                padding: EdgeInsets.only(top: 16),
                child: Text('Awaiting result...'),
              ),
              ElevatedButton(
                onPressed: () => asignar(), 
                child: Text('Calculate')
              ),
          ];
        }

        return Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              crossAxisAlignment: CrossAxisAlignment.center,
              children: children,
            ),
          );
      },
      
      );
  }
}

```
