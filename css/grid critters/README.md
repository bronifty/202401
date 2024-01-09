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


![](./media/grid-area4.png)
```css
planet {
  display: grid;
  grid-template-columns: 1fr [side-start] 100px 100px 100px [side-end];
  grid-template-rows:  1fr [bottom-start] 100px 100px 100px [bottom-end];
}

dunes {
  grid-area: bottom /side;
}
```




```css


planet {
  display: grid;
  grid-template-columns: 35% [col-start] 1fr 1fr [col-end] 35%;
  grid-template-rows: 35% [row-start] 1fr 1fr [row-end] 35%;
}

dunes {
  grid-area: row / col;
}
```


![](./media/grid-area5.png)

```css
planet {
  display: grid;
  grid-gap: 50px;
   grid-template-columns: [grass-start rocky-start] 1fr 1fr [grass-end rocky-end dunes-start] 1fr [dunes-end]; 
   grid-template-rows: [grass-row-start dune-row-start] 1fr [grass-row-end rocky-row-start] 1fr [rocky-row-end dune-row-end];
}

rocky {
  grid-area: rocky;
}

grass {
  grid-area: grass;
}

dunes {
  grid-area: dunes;
}
```

![](./media/grid-template-areas.png)
```css
planet {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-template-rows: 1fr;
  grid-template-areas: ". rocky rocky ."
  
}

rocky {
  grid-area: rocky;
}

```



![](./media/grid-template-areas2.png)
```css
planet {
  display: grid;
  grid-column-gap: 10%;
  grid-template-columns: 2fr 1fr 1fr;
  grid-template-rows: repeat(3, 1fr);
  grid-template-areas: ". . ."
  ". grass grass"
  "dunes grass grass";
}

grass {
      grid-area: grass;
}

dunes {
  grid-area: dunes;
}
```


![](./media/grid-template-areas3.png)
```css
planet {
  display: grid;
  grid-template-columns: 1fr 200px 1fr;
  grid-template-rows: 1fr 200px 1fr;
  grid-gap: 25px;
  grid-template-areas: "grass grass grass"
  "rocky rocky rocky"
  "dunes dunes dunes";
}

grass {
  grid-area: grass;
}

dunes {
  grid-area: dunes;
}
```



