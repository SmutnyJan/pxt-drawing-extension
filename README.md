# Malování

## Namespace
```
drawing
```
## Popis
Rozšíření poskytuje metody pro malování na 5×5 LED pole
 
## Metody
#### Překreslit bod
```
function redraw(): void
```
- Překreslí aktuální bod
- Bez parametrů
- Bez návratové hodnoty

#### Vymazat kresbu
```
function clear(): void
```
- Vypne všechny LED (uvedení do výchozího stavu)
- Bez parametrů
- Bez návratové hodnoty

#### Přepnout kurzor || na [%newX, %newY]
```
function toogleCursor(newX?: number, newY?: number): void
```
- Zapne/vypne blikání kurzoru (pokud si bude někdo chtít kresbu prohlédnout, mohl by kurzor překážet)
- Blok je možno rozšířit o dva parametry (x a y), záleží na obtížnosti úlohy
- Parametry:
    - nepovinný parametr nová souřadnice X (číslo)
    - nepovinný parametr nová souřadnice Y (číslo)
- Bez návratové hodnoty
 
#### Blikat kurzorem || na [%newX, %newY]
```
function blinkCursor(newX?: number, newY?: number): void
```
- Problikne kurzorem (umístí se do smyčky „opakuj stále“)
- Blok je možno rozšířit o dva parametry (x a y), záleží na obtížnosti úlohy
- Parametry:
    - nepovinný parametr nová souřadnice X (číslo)
    - nepovinný parametr nová souřadnice Y (číslo)
- Bez návratové hodnoty

#### Posunout kurzor smerem %direction
```
function moveInDirection(direction: MoveDirection): void
```
- Pohne kurzorem na danou stranu
- Parametry:
    - směr (enum)
- Bez návratové hodnoty

#### Pohyb na [%newX, %newY]
```
move(newX: number, newY: number): void
```
- Pohne kurzorem na danou souřadnici
- Parametry:
    - souřadnice X (číslo)
    - souřadnice Y (číslo)
- Bez návratové hodnoty

## Enumy
```
enum MoveDirection {
    Up = 1,
    Down = 2,
    Left = 3,
    Right = 4,
}
```

## Příklady

### Malovaní za použití zkrácených verzí bloků

#### Bloky
![Jednoduchý příklad](https://github.com/microbit-cz/pxt-drawing-extension/blob/master/images/easyexample.png)

#### Kód
```
input.onGesture(Gesture.TiltRight, function () {
    drawing.moveInDirection(MoveDirection.Right)
})
input.onGesture(Gesture.LogoDown, function () {
    drawing.moveInDirection(MoveDirection.Down)
})
input.onButtonPressed(Button.A, function () {
    drawing.toogleCursor()
})
input.onGesture(Gesture.TiltLeft, function () {
    drawing.moveInDirection(MoveDirection.Left)
})
input.onGesture(Gesture.LogoUp, function () {
    drawing.moveInDirection(MoveDirection.Up)
})
input.onButtonPressed(Button.B, function () {
    drawing.clear()
})
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    drawing.redraw()
})
basic.forever(function () {
    drawing.blinkCursor()
})
```
Demo [https://github.com/microbit-cz/pxt-drawing-demo-easy](https://github.com/microbit-cz/pxt-drawing-demo-easy)

### Malovaní za použití vlastních proměnných x a y

#### Bloky
![Těžší příklad](https://github.com/microbit-cz/pxt-drawing-extension/blob/master/images/hardexample.png)


#### Kód
```
let x = 0
let y = 0
input.onButtonPressed(Button.A, function () {
    x += -1
    if (x < 0) {
        x = 4
    }
    drawing.moveAt(x, y)
})
input.onPinPressed(TouchPin.P2, function () {
    y += 1
    if (y > 4) {
        y = 0
    }
    drawing.moveAt(x, y)
})
input.onButtonPressed(Button.AB, function () {
    drawing.toogleCursor(x, y)
})
input.onButtonPressed(Button.B, function () {
    x += 1
    if (x > 4) {
        x = 0
    }
    drawing.moveAt(x, y)
})
input.onPinPressed(TouchPin.P1, function () {
    drawing.redraw()
})
input.onGesture(Gesture.Shake, function () {
    drawing.clear()
})
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    y += -1
    if (y < 0) {
        y = 4
    }
    drawing.moveAt(x, y)
})
basic.forever(function () {
    drawing.blinkCursor(x, y)
})
```
Demo [https://github.com/microbit-cz/pxt-drawing-demo-hard](https://github.com/microbit-cz/pxt-drawing-demo-hard)

#### Metadata (slouží k vyhledávání, vykreslování)

* for PXT/microbit
<script src="https://makecode.com/gh-pages-embed.js"></script><script>makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");</script>

