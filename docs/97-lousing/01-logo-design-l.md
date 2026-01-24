# Logo Design

Designed the logo using chatgpt on 2026-01-09


## 🔍 Logo concept (locked)

* Word: **Lousing**
* Two colors:

  * Teal → left / upper bias
  * Yellow → right / lower bias
* Overall feel:

  * As if a **slanted scale / diagonal brush** painted the word
* Special rule:

  * The **dot of “i”** will be *split diagonally* into **two colors**
* Style:

  * Clean, hand-written approximation (not wobbly)
  * Filled shapes (logo-grade SVG)

✅ We’re aligned.

---

## Step 6 – Draw the letter **“L”** (only L, nothing else)

We’ll:

* Draw **one filled path**
* Slightly rounded corners
* Vertical stem + soft bottom curve
* Use **teal** for now

### Coordinate mindset

* SVG origin `(0,0)` → top-left
* Positive X → right
* Positive Y → down

We’ll draw the L starting around `(20, 20)`.

---

## 🧩 SVG path for letter “L”

Here is **only the letter L**, isolated and readable.

```svg
<svg
  width="120"
  height="120"
  viewBox="0 0 120 120"
  xmlns="http://www.w3.org/2000/svg">

  <path
    d="
      M 30 20
      C 30 20, 45 20, 45 35
      L 45 75
      C 45 85, 50 90, 60 90
      L 85 90
      C 95 90, 95 105, 85 105
      L 55 105
      C 35 105, 30 95, 30 80
      Z
    "
    fill="#9ED3CF"
  />
</svg>
```

---

## 🧠 What this path is doing (important)

The d attribute of path means data. \
We have 9 drawing commands. \
Each command moves or curves an imaginary pen to form a closed, filled polygon.

## SVG Setup
The `<svg>` element defines a 120×120 canvas with `viewBox="0 0 120 120"` for scalable rendering. `xmlns="http://www.w3.org/2000/svg"` declares the SVG namespace.[1]

## Path Commands Breakdown
```
M 30 20          // Move to (30,20) - start point, top-left of shape
C 30 20, 45 20, 45 35   // Cubic Bézier: (30,20)→(45,20)→(45,35) - gentle right curve
L 45 75          // Line to (45,75) - vertical stem down
C 45 85, 50 90, 60 90   // Cubic Bézier: (45,85)→(50,90)→(60,90) - bottom-right bulge
L 85 90          // Line to (85,90) - horizontal extension
C 95 90, 95 105, 85 105 // Cubic Bézier: (95,90)→(95,105)→(85,105) - top-right curve
L 55 105         // Line to (55,105) - leftward along top
C 35 105, 30 95, 30 80  // Cubic Bézier: (35,105)→(30,95)→(30,80) - left curve down
Z                // Close path to start point (30,20)
```

## Command Reference
| Command | Meaning | Parameters |
|---------|---------|------------|
| `M x y` | Move pen to absolute position | 2 numbers |
| `C x1 y1 x2 y2 x y` | Cubic Bézier curve | 6 numbers (control1, control2, end) |
| `L x y` | Line to absolute position | 2 numbers |
| `Z` | Close path (line to start) | None |

## Visual Flow
1. Start at (30,20)
2. Curve right to form top bulge → down stem → bottom puff → right extension
3. Curve up → left → down left side
4. `Z` connects back to origin, creating filled shape with `#9ED3CF` color.

## ✅ Why this is a good “L”

* Rounded but confident
* Not too playful
* Reads well at small sizes
* Easy to match with O, U, S later
* Scales perfectly

This will **set the handwriting style** for the rest of the letters.

---

## Next step (very intentional)

👉 **Next we will draw the letter “O”**, but:

* As a **soft oval**
* With slight thickness variation
* Same stroke logic as L

After **L + O**, everything else becomes mechanical.

Before moving on, answer just this:

**Do you want the “L” slightly taller than the rest of the letters?**
Many logos do this subtly for visual hierarchy.

Reply:

* **Yes, taller L**
* **No, uniform height**

Then we proceed to **O**.
