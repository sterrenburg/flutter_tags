# flutter_tags
[![pub package](https://img.shields.io/badge/pub-0.4.4-orange.svg)](https://pub.dartlang.org/packages/flutter_tags)
[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.me/dnag88)

Create beautiful tags quickly and easily.

**Since version 0.4.0 the structure of the code has changed radically.**
**`SelectableTags` and` InputTags` have been replaced with the Tags () widget**.
**Now it is possible to personalize every single tag, with the possibility of adding icons, images and a removal button.**
 If you still prefer the previous version, go to ![0.3.2](https://github.com/Dn-a/flutter_tags/tree/0.3.2)

## Installing
Add this to your package's pubspec.yaml file:
```dart
dependencies:
  flutter_tags: "^0.4.4"
```


## DEMO

<div align="center">
<table>
<tr>
<td style="text-align:center">
 <img width = "250px" src="https://github.com/Dn-a/flutter_tags/raw/master/repo-file/img/example0.4.0_1.gif" />
 </td>
 <td style="text-align:center">
  <img width = "250px" src="https://github.com/Dn-a/flutter_tags/raw/master/repo-file/img/example0.4.0_2.gif" />
  </td>
</tr>
</table>
</div>


## Simple usage
```dart

import 'package:flutter_tags/tag.dart';
.
.
.
List __items;
double _fontSize = 14;

@override
void initState(){
    super.initState();
    // if you store data on a local database (sqflite), then you could do something like this
    Model().getItems().then((items){
            _items = items;
        });
}

@override
Widget build(BuildContext context) {
    return Tags(
      key:_tagStateKey,
      textField: TagsTextFiled(  
        textStyle: TextStyle(fontSize: _fontSize),        
        onSubmitted: (String str) {
          // Add item to the data source.
          setState(() {
              // required
            _items.add(str);
          });
        },
      ),
      itemCount: _items.length, // required
      itemBuilder: (int index){          
            final item = _items[index];
    
            return ItemTags(
                  // Each ItemTags must contain a Key. Keys allow Flutter to
                  // uniquely identify widgets.
                  key: Key(index.toString()),
                  index: index, // required
                  title: item.title,
                  active: item.active,
                  customData: item.customData,
                  textStyle: TextStyle( fontSize: _fontSize, ),
                  combine: ItemTagsCombine.withTextBefore,
                  image: ItemTagsImage(
                    image: AssetImage("img.jpg") OR NetworkImage("https://...image.png")
                  ) OR null,
                  icon: ItemTagsIcon(
                    icon: Icons.add,
                  ) OR null,
                  removeButton: ItemTagsRemoveButton( ) OR null, 
                  onRemoved: (){
                    // Remove the item from the data source.
                    setState(() {
                        // required
                      _items.removeAt(index); 
                    });
                  },
                  onPressed: (item) => print(item),
                  onLongPressed: (item) => print(item),
            );
    
      },
    );    
}

final GlobalKey<TagsState> _tagStateKey = GlobalKey<TagsState>();
// Allows you to get a list of all the ItemTags
_getAllItem(){
    List<Item> lst = _tagStateKey.currentState?.getAllItem;
    if(lst!=null)
        lst.where((a) => a.active==true).forEach( ( a) => print(a.title));        
}
```
## Wrapped widget example
You are free to wrap ItemTags () inside another widget
```dart
Tags(  
      itemCount: items.length, 
      itemBuilder: (int index){ 
          return Tooltip(
          message: item.title,
          child:ItemTags(
            title:item.title,
          )
          );
      },
    );    
```
### Tags() parameters
|PropName|Description|default value|
|:-------|:----------|:------------|
|`columns`|*Possibility to set number of columns when necessary*|null|
|`itemCount`|*Tag number to display*|required|
|`symmetry`|*Ability to view and scroll tags horizontally*|false|
|`horizontalScroll`|*Offset drawer width*|0.4|
|`heightHorizontalScroll`|*height for HorizontalScroll to set to display tags correctly*|60|
|`spacing`|*Horizontal space between the tags*|6|
|`runSpacing`|*Vertical space between the tags*|14|
|`alignment`|*Horizontal WrapAlignment*|WrapAlignment.center|
|`runAlignment`|*Vertical WrapAlignment*|WrapAlignment.center|
|`direction`|*Direction of the ItemTags*|Axis.horizontal|
|`verticalDirection`|*Iterate Item from the lower to the upper direction or vice versa*|VerticalDirection.down|
|`textDirection`|*Text direction of  the ItemTags*|TextDirection.ltr|
|`itemBuilder`|*tag generator*||
|`textField`|*add textField*|TagsTextFiled()|

### ItemTags() parameters
* `index` - *required*
* `title` - *required*
* `textScaleFactor` - *custom textScaleFactor*
* `active` - *bool value (default true)*
* `pressEnabled` - *active onPress tag ( default true)*
* `customData` - *Possibility to add any custom value in customData field, you can retrieve this later. A good example: store an id from Firestore document.*
* `textStyle` - *textStyle()*
* `alignment` - *MainAxisAlignment ( default MainAxisAlignment.center)*
* `combine` - * ability to combine text, icons, images in different ways ( default  ItemTagsCombine.imageOrIconOrText)*
* `icon` - *ItemTagsIcon()*
* `image` - *ItemTagsImage()*
* `removeButton` - *ItemTagsRemoveButton()*
* `borderRadius` - *BorderRadius*
* `border` - *custom border-side*
* `padding` - *default EdgeInsets.symmetric(horizontal: 7, vertical: 5)*
* `elevation` - *default 5*
* `singleItem` - *default false*
* `textOverflow` - *default TextOverflow.fade*
* `textColor` - *default Colors.black*
* `textActiveColor` - *default  Colors.white*
* `color` - *default Colors.white*
* `activeColor` - *default Colors.blueGrey*
* `highlightColor` - 
* `splashColor` - 
* `colorShowDuplicate` - *default  Colors.red*
* `onPressed` - *callback*
* `onLongPressed` - *callback*
* `onRemoved` - *callback*


## Donate
If you found this project helpful or you learned something from the source code and want to thank me: 
- [![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.me/dnag88)

## Issues
If you encounter problems, open an issue. Pull request are also welcome.