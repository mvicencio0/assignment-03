## Shape Animation

### Requirements

- Write the following classes:
    - `Point`
        - Describes a point in the Euclidean plane.
            - Note: This means that the x and y values need to be either
              `float` or `double`.
        - Must be able to be initialized with no arguments, defaulting to the
          point (0,0).
            - Note: This is the same as saying that it must have a default
              constructor.  If a constructor has default values for all
              arguments, it fulfills this requirement and is considered a
              default constructor.
        - Must be able to be initialized with an x and y value.
        - Must not be possible to change the x or y value once it has been
          constructed.
            - Note: This means that the member variables containing the x and y
              values must be private (or protected), and you must implement
              getters (but not setters) for each.

    - `Shape`
        - Must contain the following pure virtual function:

          ```c++
          virtual bool contains(const Point & p) const = 0;
          ```

        - Should also contain a virtual default destructor:

          ```c++
          virtual ~Shape() {}
          ```

          This allows for child classes being handled through a pointer of
          type `Shape` to have their destructors called when the variable goes
          out of scope or is `delete`d (search "cpp polymorphism").

    - `Rectangle` and `Ellipse`
        - Must inherit from `Shape`, and be concrete classes (i.e. not abstract
          classes, i.e. they must override all `Shape`s pure virtual
          functions).

    - `Square`
        - Must inherit from `Rectangle`.

    - `Circle`
        - Must inherit from `Ellipse`.

- Write a function with the following prototype (probably in `main.cpp`):

  ```c++
  /**
   * A function to draw the `Shape`s in `s` in a terminal.
   *
   * Arguments:
   * - `count`: The number of `Shape`s in `s`.
   * - `s`: An array containing pointers to each `Shape` to draw.
   *
   * Notes:
   * - A terminal window is typically 80 columns wide by 25 lines high.
   * - The width:height aspect ratio of a terminal character is approximately
   *   1:1.9.
   */
  void draw(const int count, const Shape * const s[]);
  ```

  This function should iterate through every column on every line.  If the
  point represented by the character at that location is contained in any of
  the `Shape`s, it should print a `"*"` (or something).  If not, it should
  print a `" "` (or something).

  This function should also scale the shapes correctly, according the aspect
  ratio of the terminal characters.  It would probably be best to use several
  constants: one to represent the number of columns, one to represent the
  factor used to convert the column number to the x value represented by a
  character in that column, and similarly for the number of lines and the
  factor used to convert the line number to the corresponding y value.

  Optionally, you may also draw a border, where the top and bottom of each
  column is a `"-"` (or something), and the first and last character of each
  line is a `"|"` (or something).

- Use the following template for `main()`:

  ```c++
  int main() {
      // declare constants for the number of frames to draw and the
      // amount of time to sleep after drawing each frame

      // for each frame

          // create some shapes (with values depending on the current frame
          // number)

          // put pointers to them in an array
          //
          // for example, given a `Rectangle r` and a `Square s`:
          Shape * shapes[] = { &r, &s, };
          // this is possible because `Rectangle`s and `Squares`, and all
          // your other shapes, inherit from `Shape`

          // draw the shapes in the terminal
          //
          // for example, given the `shapes` array above:
          draw( sizeof(shapes) / sizeof(Shape *), shapes );

          // wait before drawing the next frame
          //
          // for example:
          std::this_thread::sleep_for(std::chrono::milliseconds(frameSleep));
          // if you'd like to know more about what this line is doing, look
          // up the documentation for `std::this_thread::sleep_for` and
          // `std::chrono::milliseconds()`.

      return 0;  // success
  }
  ```

  If you'd like to write your `main()` in a different way that's fine, so long
  as it accomplishes the same goal.


#### Design Constraints

- Classes must have both `.h` and `.cpp` files, with member functions defined
  in the `.cpp` files unless they are truly trivial.  If it makes sense, you
  may put multiple classes into one pair of `.h` and `.cpp` files.  I suggest
  having a `point.h` and `point.cpp`, and a `shapes.h` and `shapes.cpp`.

- `main()` must have its own `.cpp` file.  I suggest calling it `main.cpp`.

- Declare member functions and function arguments as `const` when appropriate
  (pretty much whenever possible).

- Use "include guards" in all `.h` files.  Be sure to give the preprocessor
  variable a name corresponding to the file name.  For example, in `point.h`:

  ```c++
  #ifndef POINT_H
  #define POINT_H
  // ----------------------------------------------------------------------------

  // ... everything besides the copyright information and file description

  // ----------------------------------------------------------------------------
  #endif  // POINT_H
  ```

#### Style

- Document and format your code well and consistently.
- Wrap lines at 79 or 80 columns whenever possible.
- End your file with a blank line.
- Do *not* use `using namespace std;`.  You may get around typing `std::` in
  front of things or with, e.g., `using std::cout;`.
- Include your copyright and license information at the top of every file,
  followed by a brief description of the file's contents, e.g.

  ```c++
  /* ----------------------------------------------------------------------------
   * Copyright &copy; 2015 Ben Blazak <bblazak@fullerton.edu>
   * Released under the [MIT License] (http://opensource.org/licenses/MIT)
   * ------------------------------------------------------------------------- */

  /**
   * A short program to print "Hello World!" to standard output.
   */
  ```


### Assumptions

- A terminal window is 80 columns wide by 25 lines high.
- The width:height aspect ratio of a terminal character is approximately 1:1.9.


### Notes

- If you need help creating a file in GitHub (especially if you're still using
  the web interface instead of the desktop app or the terminal) see [GitHub
  Help / Manipulating Files / Creating new
  files](https://help.github.com/articles/creating-new-files/).

- If you'd like more of a challenge, try implementing more complex shapes or
  animations.  Be creative!

- If you'd like to use a graphics library of some sort, perhaps
  [SFML](http://www.sfml-dev.org) please do!  I wanted to use one rather than
  simply printing to the terminal, but I couldn't justify making it a
  requirement (and I also didn't have enough time to experiment).


-------------------------------------------------------------------------------
[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/88x31.png)]
(http://creativecommons.org/licenses/by/4.0/)  
Copyright &copy; 2015 Ben Blazak <bblazak@fullerton.edu>  
This work is licensed under a [Creative Commons Attribution 4.0 International
License] (http://creativecommons.org/licenses/by/4.0/)  
Project located at <https://github.com/2015-fall-csuf-benblazak-cpsc-121>

