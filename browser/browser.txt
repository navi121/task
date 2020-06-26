import 'package:flutter/material.dart';
import 'package:flutter_webview_plugin/flutter_webview_plugin.dart';

void main()=>runApp(MaterialApp(
    home: Home(),
    debugShowCheckedModeBanner: false,
    theme: ThemeData(
      primarySwatch:Colors.red,
    ),
)
);
class Home extends StatefulWidget {
  @override
  _HomeState createState() => _HomeState();
}

class _HomeState extends State<Home> {
  TextEditingController controller= TextEditingController();
  FlutterWebviewPlugin flutterWebviewPlugin=FlutterWebviewPlugin();
var urlS="http://google.com";

launchUrl(){
  setState((){
    urlS = controller.text;
    flutterWebviewPlugin.reloadUrl(urlS);
  });
}
@override
  void initState() {
        super.initState();
    
    flutterWebviewPlugin.onStateChanged.listen((WebViewStateChanged wvs){
      print(wvs.type);
     
  });
  }

  @override
  Widget build(BuildContext context) {
    return WebviewScaffold(
      appBar: AppBar(
        title: TextField(
          autocorrect: true,
          autofocus: false,
          controller: controller,
          cursorColor: Colors.white,
          cursorWidth: 0.3,
          textInputAction: TextInputAction.go,
          onSubmitted: (url)=>launchUrl(),
          style: TextStyle(
            color:Colors.white),
            decoration: InputDecoration(
            border: InputBorder.none,
            hintText: "Enter the Url here",
            hintStyle: TextStyle(color:Colors.white),
            ),
          ),
actions: <Widget>[
  IconButton(
    icon: Icon(Icons.search),
    onPressed:()=>launchUrl(),
  )
],
        ),  
      url: urlS,
      withZoom: true,
    );
  }
}