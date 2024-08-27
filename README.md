<h1 align="center">
  React Native Drag and Drop
</h1>

Inspired by the [volkeno-react-native-drag-drop](https://github.com/VolkenoMakers/react-native-drag-drop) project, I decided to recreate the same functionality in React Native, with updated features and enhancements beyond the original project.

# Demo
| With Single Column                                                                                         | With Multiple Columns                                                                                          |
| ---------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| ![With Single Column](https://github.com/user-attachments/assets/a259531d-a811-43f4-9610-2a4f81ce9999) | ![With Multiple Columns](https://github.com/user-attachments/assets/7933bec4-7fd4-498a-883f-7e39e9146887) |

## Installation

- Using NPM:
  ```bash
  npm install https://github.com/Scode-Njnjas/react-native-drag-drop
  ```
  
- Using Yarn:
  ```bash
  yarn add https://github.com/Scode-Njnjas/react-native-drag-drop
  ```

## Usage

```javascript
import React from "react";
import { StyleSheet, Text, View } from "react-native";
import DragAndDrop from "react-native-drag-drop";

export default function App() {
  const [items, setItems] = React.useState([
    { id: 1, text: "Test item 1" },
    { id: 2, text: "Test item 2" },
    { id: 3, text: "Test item 3" },
    { id: 4, text: "Test item 4" },
  ]);
  const [zones, setZones] = React.useState([
    {
      id: 1,
      text: "Test zone 1",
      items: [{ id: 5, text: "Test existing item 5" }],
    },
    {
      id: 2,
      text: "Test zone 2",
    },
  ]);

  return (
    <DragAndDrop
      style={styles.container}
      contentContainerStyle={styles.contentContainerStyle}
      itemKeyExtractor={(item) => item.id}
      zoneKeyExtractor={(zone) => zone.id}
      zones={zones}
      items={items}
      itemsContainerStyle={styles.itemsContainerStyle}
      zonesContainerStyle={styles.zonesContainerStyle}
      onMaj={(updatedZones, updatedItems) => {
        setItems(updatedItems);
        setZones(updatedZones);
      }}
      itemsInZoneStyle={styles.itemsInZoneStyle}
      renderItem={(item) => {
        return (
          <View style={styles.dragItemStyle}>
            <Text style={styles.dragItemTextStyle}>{item.text}</Text>
          </View>
        );
      }}
      renderZone={(zone, children, hover) => {
        return (
          <View
            style={{
              ...styles.dragZoneStyle,
              backgroundColor: hover ? "#E2E2E2" : "#FFF",
            }}
          >
            <Text style={styles.dragZoneTextStyle}>{zone.text}</Text>
            {children}
          </View>
        );
      }}
    />
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  itemsInZoneStyle: {
    width: "100%",
  },
  contentContainerStyle: {
    padding: 20,
    paddingTop: 40,
  },
  itemsContainerStyle: {
    flexDirection: "row",
    flexWrap: "wrap",
    justifyContent: "space-between",
    alignItems: "center",
  },
  zonesContainerStyle: {
    flexDirection: "row",
    flexWrap: "wrap",
    justifyContent: "space-between",
  },
  dragItemStyle: {
    borderColor: "#F39200",
    borderWidth: 1,
    width: "47%",
    alignItems: "center",
    justifyContent: "center",
    marginVertical: 5,
    backgroundColor: "#F5F5F5",
    padding: 10,
  },
  dragItemTextStyle: {
    color: "#011F3B",
    fontWeight: "700",
    textAlign: "center",
  },
  dragZoneStyle: {
    borderColor: "#F39200",
    borderWidth: 1,
    width: "47%",
    padding: 15,
    minHeight: 130,
    marginVertical: 15,
  },
  dragZoneTextStyle: {
    position: "absolute",
    opacity: 0.2,
    zIndex: 0,
    alignSelf: "center",
    top: "50%",
  },
});
```

## Component Properties

| Property Name              | Type               | Description                                                                                                |
| -------------------------- | ------------------ | ---------------------------------------------------------------------------------------------------------- |
| **style**                  | _Object_           | Custom style for the ScrollView component                                                                  |
| **draggedElementStyle**    | _Object_           | Custom style for the dragged item                                                                          |
| **maxItemsPerZone**        | _Number_           | Maximum items inside a drop area, defaults to null (no limit)                                               |
| **itemsInZoneDisplay**     | _"row"_ or _"column"_ | Flex direction for the container of items inside a zone                                                    |
| **itemsDisplay**           | _"row"_ or _"column"_ | Flex direction for the container of draggable items                                                        |
| **itemsNumColumns**        | _Number_           | Number of columns for items                                                                                |
| **itemsInZoneNumColumns**  | _Number_           | Number of columns for items inside a zone                                                                  |
| **headerComponent**        | _ReactElement_     | Renders a header                                                                                            |
| **footerComponent**        | _ReactElement_     | Renders a footer                                                                                            |
| **contentContainerStyle**  | _Object_           | Custom style for the ScrollView `contentContainerStyle`                                                     |
| **itemKeyExtractor**       | _Function_         | Function that takes an item as a parameter and returns the item's ID                                        |
| **zoneKeyExtractor**       | _Function_         | Function that takes a zone as a parameter and returns the zone's ID                                         |
| **zones**                  | _Array_            | Array that contains the drop zones                                                                         |
| **items**                  | _Array_            | Array that contains the draggable items                                                                    |
| **itemsContainerStyle**    | _Object_           | Custom style for the container of draggable items                                                          |
| **zonesContainerStyle**    | _Object_           | Custom style for the container of the drop zones                                                           |
| **itemsInZoneStyle**       | _Object_           | Custom style for the items in the drop area                                                                |
| **onMaj**                  | _Function_         | Callback function triggered when there are changes in items or zones                                        |
| **renderItem**             | _Function_         | Function to render a draggable item                                                                        |
| **renderZone**             | _Function_         | Function to render a drop zone (important: the `children` parameter is the draggable items inside the drop zone) |

## Usage with Multiple Columns

```javascript
import React from "react";
import { StyleSheet, Text, View } from "react-native";
import DragAndDrop from "react-native-drag-drop";

export function DragDropModule() {
  const [items, setItems] = React.useState([
    { id: 1, text: "A" },
    { id: 2, text: "B" },
    { id: 3, text: "C" },
    { id: 4, text: "D" },
    { id: 5, text: "F" },
    { id: 6, text: "G" },
    { id: 7, text: "H" },
    { id: 8, text: "I" },
    { id: 9, text: "K" },
  ]);
  const [zones, setZones] = React.useState([
    {
      id: 1,
      text: "Test zone 0",
      items: [{ id: 10, text: "L" }],
    },
  ]);

  return (
    <DragAndDrop
      style={styles.container}
      contentContainerStyle={styles.contentContainerStyle}
      itemKeyExtractor={(item) => item.id}
      zoneKeyExtractor={(zone) => zone.id}
      zones={zones}
      items={items}
      onMaj={(updatedZones, updatedItems) => {
        setItems(updatedItems);
        setZones(updatedZones);
      }}
      itemsInZoneDisplay="row"
      itemsDisplay="row"
      itemsNumColumns={3}
      itemsInZoneNumColumns={2}
      renderItem={(item) => {
        return (
          <View style={styles.dragItemStyle}>
            <Text style={styles.dragItemTextStyle}>{item.text}</Text>
          </View>
        );
      }}
      renderZone={(zone, children, hover) => {
        return (
          <View style={{ marginVertical: 10 }}>
            <Text style={{ marginBottom: 5 }}>{zone.text}</Text>
            <View
              style={{
                ...styles.dragZoneStyle,
                minHeight: 150,
                backgroundColor: hover ? "#E2E2E2" : "#FFF",
              }}
            >
              {children}
            </View>
          </View>
        );
      }}
    />
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  contentContainerStyle: {
    padding: 20

,
    paddingTop: 40,
  },
  dragItemStyle: {
    borderColor: "#F39200",
    borderWidth: 1,
    alignItems: "center",
    justifyContent: "center",
    marginVertical: 5,
    backgroundColor: "#F5F5F5",
    padding: 10,
  },
  dragItemTextStyle: {
    color: "#011F3B",
    fontWeight: "700",
    textAlign: "center",
  },
  dragZoneStyle: {
    borderColor: "#F39200",
    borderWidth: 1,
    padding: 15,
  },
});
```

**ISC Licensed**
