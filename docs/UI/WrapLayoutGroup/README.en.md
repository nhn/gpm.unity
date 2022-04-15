# Multi Layout

🌏 [한국어](README.md)

## 🚩 Table of Contents

* [Overview](#overview)
* [Element](#element)
* [Sample](#sample)

## Overview

A component that aligns child elements vertically or horizontally within the UI rectangle (RectTanform).
If it goes out of range, it aligns to the next line.

![wrap.gif](images/wrap.gif)

## Element

* Child Alignment
    * Sets the sort conditions for child elements.
* Is Vertical
    * This is a factor that determines whether the alignment criterion is vertical or horizontal.
    * main
        * This is the vertical and horizontal standard line.
        * IsVertival: false
            * Perpendicular
        * IsVertival: true
            * horizontality
    * crawl
        * This is the line to align when it goes out of the main line.
        * IsVertival: false
            * horizontality
        * IsVertival: true
            * Perpendicular
* Main Inverse
    * Sort the main element in reverse.
* Cross Inverse
    * Reverses cross elements.

## Sample

* In each area, you can see the child alignment and the state aligned according to the state value.

### IsVertical : false
### Main Inverse : false
### Cross Inverse: false
![h_1.png](images/h_1.png)

---

### IsVertical : false
### Main Inverse : true
### Cross Inverse: false
![h_2.png](images/h_2.png)

---

### IsVertical : false
### Main Inverse : false
### Cross Inverse: true
![h_3.png](images/h_3.png)

---

### IsVertical : false
### Main Inverse : true
### Cross Inverse: true
![h_4.png](images/h_4.png)

---

### IsVertical : true
### Main Inverse : false
### Cross Inverse: false
![v_1.png](images/v_1.png)

---

### IsVertical : true
### Main Inverse : true
### Cross Inverse: false
![v_2.png](images/v_2.png)

---

### IsVertical : true
### Main Inverse : false
### Cross Inverse: true
![v_3.png](images/v_3.png)

---

### IsVertical : true
### Main Inverse : true
### Cross Inverse: true
![v_4.png](images/v_4.png)