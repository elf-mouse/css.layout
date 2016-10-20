## Understanding CSS Grid Systems

### 1. Resetting the Box Model

```css
.row,
.column {
    box-sizing: border-box;
}
```

### 2. Clearing Floats

```css
.row:before,
.row:after {
    content: " ";
    display: table;
}

.row:after {
    clear: both;
}
```

### 3. Defining Columns

```css
.column {
    position: relative;
    float: left;
}
```

### 4. Creating Gutters

```css
.column + .column {
    margin-left: 1.6%;
}
```

### 5. Calculating Column Widths

Now that we know the maximum number of columns, next we need to determine the width of a single (1/12) column using the following formula:

```
scw = (100 – (m * (mc – 1))) / mc
```

Where:

- scw = single column width
- m = margin (1.6%)
- mc = maximum columns (12)

When we plug in the numbers, we get a single column width of 6.86666666667%. From here we can use this number to calculate the rest of the column widths. The formula for this is:

```
cw = (scw * cs) + (m * (cs – 1))
```

Where:

- cw = column width
- scw = single column width (6.86666666667%)
- cs = column span (1-12)
- m = margin (1.6%)

Applying this formula for each of the 12 columns results in the following CSS

```css
.column-1 {
    width: 6.86666666667%;
}

.column-2 {
    width: 15.3333333333%;
}

.column-3 {
    width: 23.8%;
}

.column-4 {
    width: 32.2666666667%;
}

.column-5 {
    width: 40.7333333333%;
}

.column-6 {
    width: 49.2%;
}

.column-7 {
    width: 57.6666666667%;
}

.column-8 {
    width: 66.1333333333%;
}

.column-9 {
    width: 74.6%;
}

.column-10 {
    width: 83.0666666667%;
}

.column-11 {
    width: 91.5333333333%;
}

.column-12 {
    width: 100%;
}
```

### 6. Optimizing for Mobile Devices

```css
@media only screen and (max-width: 550px) {
    .column-1,
    .column-2,
    .column-3,
    .column-4,
    .column-5,
    .column-6,
    .column-7,
    .column-8,
    .column-9,
    .column-10,
    .column-11,
    .column-12 {
        width: auto;
        float: none;
    }

    .column + .column {
        margin-left: 0;
    }
}
```

### 7. Pulling it all Together

When we combine all the concepts and CSS, we can write HTML layout scaffolding like so:

```html
<div class="row">
    <div class="column column-4"></div>
    <div class="column column-4"></div>
    <div class="column column-4"></div>
</div>

<div class="row">
    <div class="column column-2"></div>
    <div class="column column-4"></div>
    <div class="column column-4"></div>
    <div class="column column-2"></div>
</div>
```
