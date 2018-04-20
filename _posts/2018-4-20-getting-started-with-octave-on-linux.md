---
layout: post
title: "Getting Started With Octave On Linux"
author: "Yotam S"
categories: guide
tags: [octave, linux, tutorial]
image: "/2018-4-20/post-image.png"
---

[GNU Octave](https://www.gnu.org/software/octave/) is a free tool aimed at enabling fast and easy prototyping of mathematic applications. It is a good replacement for the expansive MatLab which is why I chose it. In this little tutorial I will guide you through installing it over Linux and help you get familiar with the GUI interface and its Shell tools. 

## Differences with MatLab
Mostly Octave was build with MatLab comptability in mind. But some Octave only syntax exists. for example, MatLab accepts only single quates (`'<string>'`) while Octave accepts both single and double quates (`"<string>"`). For more information on the differences check out [this wiki page](https://en.wikibooks.org/wiki/MATLAB_Programming/Differences_between_Octave_and_MATLAB).

It's possible to run Octave in a MatLab comptability mode. This is done by using the `--traditional` or `--braindead` flags when calling octave, for example:
```bash
octave --braindead # opens the GUI in comptability mode
octave-cli --traditional # opens the command line in comptability moode
```
**Note:** You might want to edit the `~/.octaverc` file to display MatLab comptability warnings. This is done by executing:
```bash
echo "warning(\"on\",\"Octave:language-extension\");" >> ~/.octaverc
```

## The set-up
I'm using a [Lubuntu](https://lubuntu.net/) 17.10 (64 Bit) virtual machine, installed with [VirtualBox](https://www.virtualbox.org/). Lubuntu is one of the smaller distro's based on Ubuntu. Therefore it is also compatible with `sudo apt-get` and all the Ubuntu repositories. Out of the box there are still some things you must install before getting Octave. I recommend running the following set of commands:
```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install gcc make build-essential
```
And remember to install the VirtualBox Guest additions for better integration.

__Note:__ If you are using a non American locale as me (can check with the shell command `locale`), it is good practice to declare it UTF-8. In my case I had to run the command:
```bash
sudo update-locale LANG=en_IL.UTF-8
```

## Installing Octave
In order to install Octave, head over to [their website](https://www.gnu.org/software/octave/) and download the version that fits you. If you chose to install the Linux version, just run the following command in the terminal:
```bash
sudo apt-get install octave
```
And Vualla you have successfully installed  GNU Octave!

## Octave basics
Octave can be used in two ways within Linux:
1. The command line interface, by running the command `octave-cli`.
2. The user interface, through the 'start menu' or by running the command `octave`.

I will be using the GUI form. But in the command line all the command are identical. The only two commands worth mentioning are:
```bash
PS1(">> ") # converts the line prefix string to '>> '
clc # clear the screen (like 'clear')
```
### Math operations
Same as any other IDE, but also supports element-wise operations.

| Oper.           | Math            | Description             |
| --------------- | --------------- | ----------------------- |
| x + y           | $$x + y$$       | Plus operator           |
| x - y           | $$x - y$$       | Minus operator          |
| x * y           | $$x \cdot y$$   | Multiply operator       |
| x \ y           | $$\frac{x}{y}$$ | Right-devision operator |
| x^y *or* x**y | $$x^y$$         | Exponent operator       |

All of the above also exist in an element-wise action. by using the `.` (dot) prefix. For example `x .+ y` is the element-wise `+`.

### Matrices and vectors
A vector or matrix are created in a similar fassion to other programming languages. For example vectors:
```m
>> v = [1 2 3 4 5]
v = 
     1 2 3 4

>> v = [1; 2; 3; 4; 5]
v =
     1
     2
     3
     4
```
And matrices, where every row is seperated by `;`:
```m
>> M = [1 2; 3 4];
M =
     1  2
     3  4
```
There are a few special functions for matrix/vector creation. Such as:
- `ones(n, m)` - An $$n \times m$$ matrix of 1's
- `zeros(n, m)` - An $$n \times m$$ matrix of 0's
- `eye(n)`, `eye(n, m)` - An $$n \times n$$ or $$n \times m$$ matrix of 0's with 1's on the main diagonal (identity matrix)
- `rand(n, m)` - An $$n \times m$$ matrix of **uniformly** distributed random elements
- `randn(n, m)` - An $$n \times m$$ matrix of **normally** distributed random elements

### Colon operator
A great tool for defining a set of values in a range. Used also for selection of a part of a matrix.
```m
>> v = 1 : 5
v = 
     1 2 3 4 5

>> v = 4 : 2 : 10
v = 
     4 6 8 10
```
**Note:** The second example is defined as `<start> : <increment size> : <end>`.

### Indexing
Accessing certain elements from a matrix/vector can be achieved with indexing. It is somewhat similar to the way indexing work in *Python NumPy*.
```m
>> M = [1 2; 3 4]
M = 
     1 2
     3 4
```
- `M(1,1)` will return 1
- `M(1, [1,2])` will return [1 2]
- `M(2, 1:2)` will return [3 4]
- `M(2, :)` will return [3 4]

**Note:** Similar to Python, the colon operator here works like 'select all'.

### Other functions
I recommend taking a look at the [documentation](https://octave.org/doc/v4.2.2/) for more available functions. But here are a few extra functions that are available in Octave:
- `sprintf(<string>, <arguments> ...)` - Same as in C, use this to print a formatted string to the screen (terminal).
- `ceil(x)`, `floor(x)`, `round(x)` - Same operations as in Python.
- `max(x)`, `min(x)` - Highest or lowest value in a vector.

## The Octave user interface
When opening the Octave user interface, you will be greeted with the `Command Window` view (which is basically a terminal):
![octave main screen]({{ site.baseurl }}/assets/img/2018-4-20/octave-main-interface.png "The terminal view within Octave")

In the bottom-right tabs the `Editor` and `Documentation` views are also available:
![octave bottom-right tabs]({{ site.baseurl }}/assets/img/2018-4-20/octave-view-tabs.png "The bottom-right tabs")

The `Editor` view allows the creation and editing of a script which can be ran within the editor or through the `Command Window` or an external shell window with the command `octave-cli  <path to script>/<script name>.m`. The editor enables Debug options like setting breakpoints and running in debug mode. For example:
![octave debug controls]({{ site.baseurl }}/assets/img/2018-4-20/octave-debug-controls.png "The Octave editor debug controls")

## Conclusion
There you have it. Just a quick overview and set-up of GNU Octave. I hope it helped you somehow. Enjoy playing around with Octave! <i class="fa fa-smile-o" aria-hidden="true" />

Finally, here's a sombrero plot for you:
![octave sombrero plot]({{ site.baseurl }}/assets/img/2018-4-20/octave-sombrero-plot-only.png "An Octave plot featuring a sombrero in 3D")

And the code to create it:
```m
tx = ty = linspace (-8, 8, 41)';
[xx, yy] = meshgrid (tx, ty);
r = sqrt (xx .^ 2 + yy .^ 2) + eps;
tz = sin (r) ./ r;
mesh (tx, ty, tz);
xlabel ('tx');
ylabel ('ty');
zlabel ('tz');
title ('3-D Sombrero plot');
```
