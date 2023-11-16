# react-native-image-mapper-lelli

React Native component to allow clickable areas on an image

### Setup
```
$ npm i react-native-image-mapper-lelli --save
```

### Usage

Import the `ImageMapper` component from `react-native-image-mapper-lelli` and use it as seen below:

```jsx
import React, { useEffect, useState } from 'react';
import ImageMapper from 'react-native-image-mapper-lelli'

export default function InspeccionDigital() {
  const [imageSource, setImageSource] = useState('');

  useEffect(() => {
    // Obtén una imagen de Lorem Picsum
    const loremPicsumUrl = 'https://picsum.photos/250/500';
    setImageSource(loremPicsumUrl);
  }, []);

  const onAnyAreaPress = (item, idx, event) => {
    // Manejar la lógica cuando se hace clic en cualquier área
    console.log('Área clickeada:', item);
  };

  return (
    <ImageMapper
      imgHeight={500}
      imgWidth={250}
      imgSource={{ uri: imageSource }}
      imgMap={[
        {
          id: 'area1',
          shape: 'rectangle',
          x1: 50,
          y1: 50,
          x2: 150,
          y2: 150,
          fill: 'rgba(255, 0, 0, 0.5)', // Rojo
        },
        {
          id: 'area2',
          shape: 'circle',
          x1: 200,
          y1: 100,
          radius: 30,
          fill: 'rgba(255, 0, 0, 0.5)', // Rojo
        },
      ]}
      onPress={(item, idx, event) => onAnyAreaPress(item, idx, event)}
      selectedAreaId="my_area_id"
    />
  );
}
```

### Properties

|Prop Name|Type|Description|Example|
|---|---|---|---|
|**imgSource**|*string*|Image source url| **required**|
|**imgMap**|*array*|Mapping for image| See below |
|**selectedAreaId**|*string* or *array*|ID of the currently selected area or array of ids| `'areaOne'` or `['areaOne', 'areaTwo']`|
|**imgWidth**|*number*|Image width|`Displayed width`|
|**imgHeight**|*number*|Image height|`Displayed height`|
|**multiselect**|*boolean*| Defaults to `false`. Allows for tracking of multiple selections.|`true` or `false`|

**When `multiselect` is set to `true`, `selectedAreaId` must be an array of ids rather than a string**

|Props callbacks|Called on|Signature|
|---|---|---|
|**onPress**|Click on an area in image|`(item: object, index: number, event: object)`|


**`imgMap` is an object describing touchable areas in the image.**

|Property|Type|Description|
|---|:---:|---|
|**id**|*string*|ID of the item used for selected or not selected|
|**name**|*string*|Name of the item|
|**shape**|*string*|**Required** - Either `rectangle` or `circle`|
|**prefill**|*string*|rgba(255, 255, 255, 0.5)|
|**fill**|*string*|rgba(255, 255, 255, 0.5)|
|**x1**|*number*|**Required** - Top Left X coordinate in rectangle or Center X coordinate in circle|
|**y1**|*number*|**Required** - Top Left Y coordinate in rectangle or Center Y coordinate in circle|
|**x2**|*number*|**Required for Rectangle unless `width` (below) is specified** - Bottom Left X coordinate in rectangle|
|**y2**|*number*|**Required for Rectangle unless `height` (below) is specified** - Bottom Left Y coordinate in rectangle|
|**width**|*number*|**Required for Rectangle unless `x2` (above) is specified** - Width of rectangle|
|**height**|*number*|**Required for Rectangle unless `y2` (above) is specified** - Height of rectangle|
|**radius**|*number*|**Required for Circle** - Radius of circle|

### License
Copyright (c) 2023 Franco Lelli
MIT License
See LICENSE for specifics
