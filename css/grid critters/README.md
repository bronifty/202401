https://mastery.games/gridcritters/chapter/3/level/13

![](./media/grass.png)
```css
planet {
  display: grid;
  grid-template-columns: 1fr repeat(5, [grass] 50px) [grass] 1fr;
  grid-template-rows: 1fr;
}

grass {
  grid-column: grass 2 / grass 5;
}
```

### Grid Area
![](./media/grid-area.png)
```css
planet {
  display: grid;
  grid-template-columns: [left] 190px 190px [right];
  grid-template-rows: [top] 1fr 1fr 1fr 1fr [bottom];
}

dunes {
  grid-area: top / left / bottom / right;
}
```

![](./media/grid-area2.png)
```css
planet {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 1fr 1fr 1fr;
}

dunes {
 grid-area: 2 / 2 / 4 / 4; 
}
```

![](./media/grid-area3.png)
```css
planet {
  display: grid;
  grid-template-columns: 20% 1fr 20%;
  grid-template-rows: 1fr 1fr 1fr 1fr 1fr;
  grid-column-gap: 50px;
}

grass {
 grid-area: 1 / 2 / -1  / -1;
}
```


