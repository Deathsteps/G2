# Annotation

## Text Annotation

```js
G2.render({
  type: 'view',
  width: 640,
  transform: [
    {
      type: 'fetch',
      url: 'https://gw.alipayobjects.com/os/antfincdn/ulQpndlrT%26/line.json',
    },
  ],
  scale: {
    x: { nice: true, tickCount: 15 },
    y: { guide: null },
  },
  children: [
    {
      type: 'line',
      encode: {
        x: (d) => new Date(d.date),
        y: 'value',
      },
    },
    {
      type: 'annotation.text',
      transform: [
        {
          type: 'filterBy',
          fields: ['date'],
          callback: (d) => d === 'March 2008' || d === 'March 2019',
        },
      ],
      encode: {
        x: (d) => new Date(d.date),
        y: 'value',
        text: (d) =>
          d.date === 'March 2019'
            ? 'The most visits were in March 2019 with 8.30M in total'
            : 'There was a drop in number of visits in early 2008 which have been due to The Greet Recession',
      },
      style: {
        fill: 'black',
        fontSize: 10,
        textAlign: 'right',
        textBaseline: 'middle',
        dy: 8,
        dx: -20,
        wordWrap: true,
        wordWrapWidth: 100,
        connector: { lineDash: [2, 1], stroke: '#416180', lineWidth: 1 },
        background: {
          fill: '#FFF',
          padding: [2, 2],
        },
      },
    },
  ],
});
```

## Badge Annotation

```js
G2.render(
  {
    type: 'view',
    width: 640,
    transform: [
      {
        type: 'fetch',
        url: 'https://gw.alipayobjects.com/os/antfincdn/jjAX4HPWB9/sales.json',
      },
    ],
    scale: {
      x: { nice: true, tickCount: 15 },
      y: { guide: null },
      color: { guide: null },
    },
    children: [
      {
        type: 'line',
        encode: {
          x: (d) => new Date(d.date),
          y: 'sales',
          color: 'fruit',
        },
      },
      {
        type: 'annotation.text',
        encode: {
          x: (d) => new Date(d.date),
          y: 'sales',
          text: 'sales',
          color: 'fruit',
          shape: 'annotation.badge',
        },
        style: {
          size: 20,
        },
      },
    ],
  },
  {},
);
```

## Connector Annotation

```js
G2.render(
  {
    type: 'view',
    height: 300,
    data: [
      { genre: 'Sports', sold: 275 },
      { genre: 'Strategy', sold: 115 },
      { genre: 'Action', sold: 120 },
      { genre: 'Shooter', sold: 150 },
      { genre: 'Other', sold: 350 },
    ],
    children: [
      {
        type: 'interval',
        encode: {
          x: 'genre',
          y: 'sold',
          color: 'genre',
        },
      },
      {
        type: 'annotation.connector',
        data: [
          { x1: 'Strategy', x2: 'Action', y1: 115, y2: 120 },
          { x1: 'Other', x2: 'Shooter', y1: 350, y2: 150 },
        ],
        encode: {
          x: ['x1', 'x2'],
          y: ['y1', 'y2'],
        },
        style: {
          stroke: '#979797',
        },
      },
    ],
  },
  {},
);
```