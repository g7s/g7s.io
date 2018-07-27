+++
title = "Units and measurements"
description = "Some notes on measurements."
date = "2018-07-27T10:30:29+03:00"
tags = ["units", "clojure"]
+++


# Introduction


## Properties

For a system one can define properties that describe the system in some sense. For example consider
the system of the display you are reading this on. This system has many qualitative characteristics
such as how large it is, how luminous it is, how often it refreshes the displayed image etc. Some of
these system properties are also measurable:

<i class="definition">
A system property is **measurable** if by using a reproducible process, one can associate it with a
real number.
</i>

For example the properties of a physical system (the physical properties) are all measurable.
Here we will examine only *measurable* properties, so from now on a property is implied to be measurable.

One can define properties in terms of other properties of the system. For example on a physical
system one can define *pressure* to be: force per unit area; force on the other hand can be defined
in terms of other properties such as length, mass and time.

<i class="definition">
A system property is **fundamental** if it cannot be described in terms of other properties of
the system.
</i>


## Units

From the early days humans used a "comparison process" in order to quantify properties such
as length, mass etc. This comparison process involves the existence of what we call a unit
of measurement.

<i class="definition">
A **unit of measurement** is an arbitrarily defined quantity of a property that can be
obtained by a reproducible process.
</i>

*Note*: Because a unit of measurement is arbitrarily defined, many different units of measurement that
are associated with the same physical property have been used over the years. This led to the
need for defining conversion rules between those units and groupings of units that we call
systems of measurement. Well known and used systems of measurement include the
[International System of Units](https://en.wikipedia.org/wiki/Metric_system), the
[Imperial System](https://en.wikipedia.org/wiki/Imperial_units), the
[USCS](https://en.wikipedia.org/wiki/United_States_customary_units) and several others. The above
systems of measurement are all "in use" and that has led to disasters like the destruction of
NASAs [Mars Climate Orbiter](https://en.wikipedia.org/wiki/Mars_Climate_Orbiter) and several
[airplane](https://en.wikipedia.org/wiki/Gimli_Glider)
[accidents](https://en.wikipedia.org/wiki/Korean_Air_Cargo_Flight_6316).


<i class="definition">
If a unit of measurement is associated with a fundamental property then it is called a
**base unit of measurement**. All other units are called **derived units of measurement**.
</i>

For any system one can define its fundamental properties, for example for a physical system
those are:

* Length ($L$)
* Mass ($M$)
* Time ($T$)
* Temperature ($\Theta$)
* Electric charge ($Q$)
* Amount of substance ($N$)
* Luminosity ($J$)


## Measurement

The measurement process of a property is done by comparing the occuring quantity with the unit
of measurement. We call the result of this process a **measurement** and it is tied to the unit
that was used for comparison.


# Representation

We will denote a unit by bold letters. For example $\textbf{ft}$ is going to denote a unit.
Every unit $\textbf{u}$ can be expressed as a combination (see [derivation](#derivation)) of
the base units and thus we can define its dimensions to be the way a unit is composed from
those base units.

<i class="definition">
The **dimension** of a unit $\textbf{u}$ is a $n$-element vector
\begin{equation}
\vec{d}_{\textbf{u}} = \begin{bmatrix} d\_{u1} \dots d\_{un} \end{bmatrix}
\end{equation}
with elements $d\_{ui} \in \mathbb{Z}$ that are the exponents in the way the unit has been
composed from the base units.
</i>

<!--<span class="example">
Consider the unit **ft** that measures length and the unit **h** that measures
time. Their dimensions are:

<div>
\begin{align*}
\vec{d}_{\textbf{ft}} &= \begin{bmatrix} 1 & 0 & 0 & 0 & 0 & 0 & 0 \end{bmatrix} \\
\vec{d}_{\textbf{h}} &= \begin{bmatrix} 0 & 0 & 1 & 0 & 0 & 0 & 0 \end{bmatrix} \\
\end{align*}
</div>

Therefore the dimension for the unit $\textbf{ft/h}$ is:
<div>
\begin{equation}
\vec{d}_{\textbf{ft/h}} = \begin{bmatrix} 1 & 0 & -1 & 0 & 0 & 0 & 0 \end{bmatrix}
\end{equation}
</div>
</span>-->


<i class="definition">
A unit $\textbf{u}$ is **dimensionally equivalent** to another unit $\textbf{v}$ iff
$\vec{d}\_{\textbf{u}} = \vec{d}\_{\textbf{v}}$ and we write
\begin{equation}
\textbf{u} \sim \textbf{v}
\tag{d.1} \label{dim.eq}
\end{equation}
The binary relation $\sim$ is an equivalence relation in the set of all units $\mathbb{U}$.
</i>

*Note*: One could say that any two dimensionally equivalent units measure the same system
property but that is not true. Consider for example that torque and energy have the same
dimensions but are two very different physical properties.

<hr/>

We will represent a unit of measurement $\textbf{u}$ as a pair of a function $u\_{\textbf{v}}$
that converts the magnitude of a measurement, expressed in this unit, to a magnitude expressed
in another unit $\textbf{v}$, that we take as a *reference unit*, together with its dimensions:
<div>
\begin{equation}
\textbf{u} \overset{\underset{\mathrm{def}}{}}{=} \(\vec{d}\_{\textbf{u}}, u\_{\textbf{v}}\)
\end{equation}
</div>

The function $u\_{\textbf{v}}$ is called the **conversion function** from $\textbf{u}$ to
$\textbf{v}$.


## The conversion function

For our further discussion we state some axioms / assumptions about the conversion function.

<div class="axiom">
A conversion function $u_\textbf{v}$ is unary and its domain $D_{u_\textbf{v}}$ and range
$R_{u_\textbf{v}}$ are subsets of the real numbers

<div>
\begin{equation}
u_{\textbf{v}}: \quad x \in D_{u_{\textbf{v}}} \subseteq \mathbb{R} \ \longmapsto
                 \ u_{\textbf{v}}(x) \in R_{u_{\textbf{v}}} \subseteq \mathbb{R}
                 \tag{c.1} \label{conv.fun.axiom.1}
\end{equation}
</div>
</div>

This axiom stems from the fact that generally a measurement is just a magnitude expressed
in some units, so the dependent variables of $u_\textbf{v}$ should only be the magnitude of
a measurement.

The domain $D\_{u\_\textbf{v}}$ and the range $R\_{u\_\textbf{v}}$ of the conversion function
$u\_\textbf{v}$ should be subsets of the real numbers because the magnitude of a measurement is
a real number.

<div class="axiom">
For a conversion function $u_\textbf{v}$ its inverse $u^{-1}_{\textbf{v}}$ exists and it holds that
</div>

<div>
\begin{equation}
u^{-1}_{\textbf{v}} \equiv v_{\textbf{u}}
\tag{c.2} \label{conv.fun.axiom.2}
\end{equation}
</div>

Axiom $\ref{conv.fun.axiom.2}$ exists because conversions from unit $\textbf{u}$ to unit
$\textbf{v}$ should be reversible, therefore $u^{-1}\_{\textbf{v}}$ should always exist.


# Derivation

Derivation of units from other units is accomplished through the definition of certain relations
between units of measurement.

<div class="definition">
Let $\textbf{a} = (\vec{d}_{\textbf{a}}, a_{\textbf{v}})$ and
$\textbf{b} = (\vec{d}_{\textbf{b}}, b_{\textbf{w}})$ be two units. Their <strong>relative change</strong>
is a new unit $\textbf{c}$:
</div>

<div>
\begin{equation}
\textbf{a}\textbf{/}\textbf{b} \equiv \textbf{c} \overset{\underset{\mathrm{def}}{}}{=}
\left( \vec{d}_{\textbf{c}}, c_{\textbf{v/w}} \right) =
\left( \vec{d}_{\textbf{a}} - \vec{d}_{\textbf{b}},
\frac{\delta a_{\textbf{v}}}{\delta b_{\textbf{w}}} \right) \tag{d.1} \label{relative.change.def}
\end{equation}

where the derived dimension $\vec{d}_{\textbf{c}}$ equals $\vec{d}_{\textbf{a}} - \vec{d}_{\textbf{b}}$
and the derived conversion function $c_{\textbf{v/w}}$ is defined as
$\delta a_{\textbf{v}} / \delta b_{\textbf{w}}$.
</div>

It is known that for a differentiable function $f(x)$ that
$\delta f(x) = f^{\prime}(x)\delta x$, so if we pose the extra restriction that the conversion
function is differentiable (actually infinitely differentiable) we can define:

<div>
\begin{align*}
\delta a_{\textbf{v}}(x, \delta x) &= a^{\prime}_{\textbf{v}}(x) \delta x \\
\delta b_{\textbf{w}}(y, \delta y) &= b^{\prime}_{\textbf{w}}(y) \delta y \\
\end{align*}
</div>

and therefore

<div>
\begin{align*}
\frac{\delta a_{\textbf{v}}}{\delta b_{\textbf{w}}}(x, y, \delta x, \delta y)
&= \frac{a^{\prime}_{\textbf{v}}(x) \delta x}{b^{\prime}_{\textbf{w}}(y) \delta y} \Leftrightarrow \\
\frac{\delta a_{\textbf{v}}}{\delta b_{\textbf{w}}}(m, x, y)
&= m\frac{a^{\prime}_{\textbf{v}}(x)}{b^{\prime}_{\textbf{w}}(y)} \tag{d.2}
\label{relative.change.conv.fun} \\
\end{align*}
</div>

where $m = \frac{\delta x}{\delta y}$ is the magnitude of the measurement expressed in
$\textbf{c}$. Now, taking into account $\ref{conv.fun.axiom.1}$ (i.e. a conversion function
should be [unary](#the-conversion-function)), we have from $\ref{relative.change.conv.fun}$ that

<div>
\begin{align*}
\frac{\partial}{\partial x} \frac{\delta a_{\textbf{v}}}{\delta b_{\textbf{w}}}(m, x, y)
&= 0 \Leftrightarrow \\
\frac{\partial}{\partial x} m\frac{a^{\prime}_{\textbf{v}}(x)}{b^{\prime}_{\textbf{w}}(y)}
&= 0 \Leftrightarrow \\
m\frac{a^{\prime\prime}_{\textbf{v}}(x)}{b^{\prime}_{\textbf{w}}(y)}
&= 0 \Leftrightarrow \\
a^{\prime\prime}_{\textbf{v}}(x)
&= 0 \Leftrightarrow \\
a_{\textbf{v}}(x)
&= c x + d
\end{align*}

where $c \in \mathbb{R}^*$ and $d \in \mathbb{R}$.
</div>

Applying the same for the $y$ variable we have that

<div>
\begin{equation}
b_{\textbf{w}}(y) = e y + h
\end{equation}

where $e \in \mathbb{R}^*$ and $h \in \mathbb{R}$.
</div>


What the above say is that given our assumptions / restrictions about a conversion function and
in order to be able to define the *relative change* $\ref{relative.change.def}$ (or in fact any
derived unit) a conversion function from $\textbf{u}$ to $\textbf{v}$ should be of the form

<div>
\begin{align*}
    u_{\textbf{v}}(x) &= c x + d \tag{d.3} \label{conversion.fun.gen} \\
    u^{-1}_{\textbf{v}}(y) \equiv v_{\textbf{u}}(y) &= \frac{1}{c} y - d
\end{align*}
</div>

where $c \in \mathbb{R}^*, d \in \mathbb{R}$.

Therefore given that

<div>
\begin{align*}
a_{\textbf{v}}(x) &= c x + d \\
b_{\textbf{w}}(y) &= e y + h \tag{d.3a}
\label{conversion.fun}
\end{align*}
</div>


relation $\ref{relative.change.conv.fun}$ becomes

<div>

\begin{equation}
\boxed{
\frac{\delta a_{\textbf{v}}}{\delta b_{\textbf{w}}}(m) = m\frac{c}{e}
}
\tag{d.4}
\label{relative.change.fun.final}
\end{equation}
</div>


<div class="definition">
Let $\textbf{a} = (\vec{d}_{\textbf{a}}, a_{\textbf{v}})$ and
$\textbf{b} = (\vec{d}_{\textbf{b}}, b_{\textbf{w}})$ be two units. Their
<strong>multiplicative change</strong> is a new unit $\textbf{c}$:
</div>

<div>
\begin{equation}
\textbf{a}\cdot\textbf{b} \equiv \textbf{c} \overset{\underset{\mathrm{def}}{}}{=}
\left( \vec{d}_{\textbf{c}}, c_{\textbf{vw}} \right) =
\left( \vec{d}_{\textbf{a}} + \vec{d}_{\textbf{b}},
\delta a_{\textbf{v}} \delta b_{\textbf{w}} \right) \tag{d.5} \label{multiplicative.change.def}
\end{equation}
</div>

Following a similar approach with the relative change, one can conclude, given $\ref{conversion.fun}$,
that for the conversion function $\delta a\_{\textbf{v}} \delta b\_{\textbf{w}}$ the following is true

<div>
\begin{equation}
\boxed{
\delta a_{\textbf{v}} \delta b_{\textbf{w}}(m) = mce
}
\tag{d.6}
\label{multiplicative.change.fun.final}
\end{equation}
</div>


<div class="definition">
Let $k \in \mathbb{N}^*$ be a non-zero natural number and
$\textbf{a} = (\vec{d}_{\textbf{a}}, a_{\textbf{v}})$ a unit. The $k$ <strong>exponential change</strong>
of $\textbf{a}$ is a new unit $\textbf{c}$:
</div>

<div>
\begin{equation}
\textbf{a}^k \equiv \textbf{c} \overset{\underset{\mathrm{def}}{}}{=}
\left( \vec{d}_{\textbf{c}}, c_{\textbf{v}^k} \right) =
\left( k \vec{d}_{\textbf{a}},
\underbrace{\delta a_{\textbf{v}} \cdots \delta a_{\textbf{v}}}_{\text{k terms}} \right)
\tag{d.7} \label{exponential.change.def}
\end{equation}
</div>

Again, taking into account $\ref{conversion.fun}$ one can derive that the
conversion function $c_{\textbf{v}^k}$ is

<div>
\begin{equation}
\boxed{
\underbrace{\delta a_{\textbf{v}} \cdots \delta a_{\textbf{v}}}_{\text{k terms}}(m) = mc^k
}
\tag{d.8} \label{exponential.change.fun.final}
\end{equation}
</div>

*Note*: The $k$ exponential change could be derived immediatelly from the multiplicative change
applied $k$ times on the same unit.

Lastly we define the prefix of a unit, purely as a scaling operation onto the conversion
function

<i class="definition">
Let $p$ be a symbol that has an associated factor $|p| \in \mathbb{R}^*$.
The **prefix** $p$ of a unit $\textbf{a}$ is a new unit $\textbf{c}$:
</i>

<div>
\begin{equation}
p\textbf{a} \equiv \textbf{c} \overset{\underset{\mathrm{def}}{}}{=}
\left( \vec{d}_{\textbf{c}}, c_{\textbf{v}} \right) =
\left(\vec{d}_{\textbf{a}},
|p| a_{\textbf{v}} \right)
\tag{d.9} \label{prefix.def}
\end{equation}
</div>

An example [metric prefix]
(https://en.wikipedia.org/wiki/Metric_prefix) is $T$ (tera) with an associated factor of $10^{12}$.



# Implementation

Let's represent a unit with a 3-element vector. The first element is the dimensions of the
unit, the second the slope of the conversion function and the third the y-intercept of the conversion
function $\ref{conversion.fun.gen}$

```clojure
(defn make-unit
  ([dimension slope]
   (make-unit dimension slope 0))
  ([dimension slope y-intercept]
   ^{:type ::unit}
   (vector dimension slope y-intercept)))
```

Next we define the selectors `dimensions`, `slope`, `y-intercept` and the `conv-fn`, `inv-conv-fn`
which are the conversion function for a unit and its inverse (see $\ref{conversion.fun.gen}$)

```clojure
(defn dimensions
  "The dimensions vector of a unit."
  [unit]
  (get unit 0))

(defn slope
  [unit]
  (get unit 1))

(defn y-intercept
  [unit]
  (get unit 2))

(defn conv-fn
  "The conversion function of a unit."
  [unit]
  (fn [x] (+ (* x (slope unit)) (y-intercept unit))))

(defn inv-conv-fn
  "The inverse conversion function of a unit."
  [unit]
  (fn [x] (- (/ x (slope unit)) (y-intercept unit))))
```

It is trivial now to implement the operations
$\ref{relative.change.def}, \ref{multiplicative.change.def}, \ref{exponential.change.def}$
and $\ref{prefix.def}$

```clojure
(defn div
  "The relative change operation."
  ([u] u)
  ([u1 u2]
   (make-unit (mapv - (dimensions u1) (dimensions u2))
              (/ (slope u1) (slope u2))))
  ([u1 u2 & rest]
   (reduce div (div u1 u2) rest)))

(defn mult
  "The mutliplicative change operation."
  ([u] u)
  ([u1 u2]
   (make-unit (mapv + (dimensions u1) (dimensions u2))
              (* (slope u1) (slope u2))))
  ([u1 u2 & rest]
   (reduce mult (mult u1 u2) rest)))

(defn exp
  "The k exponentiation operation."
  ([u k]
   (make-unit (mapv #(* % k) (dimensions u))
              (math/expt (slope u) k))))

(defn prefix
  "The prefix operation."
  [u p]
  (make-unit (dimensions u) (* (slope u) p) (* (y-intercept u) p)))
```

In order to be able to convert a magnitude from one unit to another we need a predicate function
that tests whether two units are dimensionally equivalent $\ref{dim.eq}$ (again, note that this
condition is only *necessary* and not sufficient for whether the conversion can be performed):

```clojure
(defn dim-eq
  "Check if the units are dimensionally equivalent."
  ([u] true)
  ([u1 u2] (= (dimensions u1) (dimensions u2))))
```

What remains now is a function that converts a magnitude from one unit to another unit. In order to
be able to do this both the units conversion functions must convert a magnitude to a same reference
unit. For example later when we see how all these apply to the physical system we choose the SI as the
reference system.

```clojure
(defn convert
  "Convert a magnitude from a unit to another. Throw exception if not dimensionally equivalent."
  [magnitude u1 u2]
  (if (dim-eq u1 u2)
    (-> magnitude
        ((conv-fn u1))
        ((inv-conv-fn u2)))
    (throw (Exception. "Units have different dimensions."))))
```


## The physical system - an example

As an example we define units that measure physical properties and we perform conversions between them.
We use the SI as a reference system, which means that all of the conversion functions are defined to
convert the magnitude from the unit to the corresponding SI unit.

```clojure
(def prefixes
  {:Y  1e24
   :Z  1e21
   :E  1e18
   :P  1e15
   :T  1e12
   :G  1e9
   :M  1e6
   :k  1e3
   :h  1e2
   :da 1e1
   :d  1e-1
   :c  1e-2
   :m  1e-3
   :μ  1e-6
   :n  1e-9
   :p  1e-12
   :f  1e-15
   :a  1e-18
   :z  1e-21
   :y  1e-24})

(def meter (make-unit [1 0 0 0 0 0 0] 1))
(def foot (make-unit [1 0 0 0 0 0 0] 0.3048))
(def inch (make-unit [1 0 0 0 0 0 0] 0.0254))
(def yard (make-unit [1 0 0 0 0 0 0] 0.9144))
(def mile (make-unit [1 0 0 0 0 0 0] 1609.344))
(def gram (make-unit [0 1 0 0 0 0 0] 1e-3))
(def pound (make-unit [0 1 0 0 0 0 0] 0.45359237))
(def ounce (make-unit [0 1 0 0 0 0 0] 0.0283495231))
(def second (make-unit [0 0 1 0 0 0 0] 1))
(def minute (make-unit [0 0 1 0 0 0 0] 60))
(def hour (make-unit [0 0 1 0 0 0 0] 3600))
(def day (make-unit [0 0 1 0 0 0 0] 86400))
(def kelvin (make-unit [0 0 0 1 0 0 0] 1))
(def celsius (make-unit [0 0 0 1 0 0 0] 1 273.15))
(def fahrenheit (make-unit [0 0 0 1 0 0 0] 5/9 459.67))
(def joule (make-unit [2 1 -2 0 0 0 0] 1))
(def calorie (make-unit [2 1 -2 0 0 0 0] 4.184))
(def newton (make-unit [1 1 -2 0 0 0 0] 1))
(def dyn (make-unit [1 1 -2 0 0 0 0] 1e-5))
(def kilopond (make-unit [1 1 -2 0 0 0 0] 9.80665))
(def poundal (make-unit [1 1 -2 0 0 0 0] 0.138255))
(def poundforce (make-unit [1 1 -2 0 0 0 0] 4.448222))
(def watt (make-unit [2 1 -3 0 0 0 0] 1))
(def hertz (make-unit [0 0 -1 0 0 0 0] 1))
(def km-per-hr (div (prefix meter (prefixes :k)) hour))
(def miles-per-hour (div mile hour))
```

Having defined these few units we can calculate conversions between them. For example we can
convert 3.5 ounces to kg:

```clojure
(convert 3.5 ounce (prefix gram (prefixes :k))) ;; = 0.09922333085
```

We can convert something more exotic like heat transfer coefficient measurements. Say that we have
$43\frac{W}{m^2K}$ and we want to convert it to $\frac{kcal}{ft^2h^{\circ}C}$. First we define the
units

```clojure
(def watt-per-sq-meter-kelvin (div watt (mult (exp meter 2) kelvin)))
(def kcal-per-sq-foot-celsius-hour (div (prefix calorie (prefixes :k))
                                        (mult (exp foot 2)
                                              (mult hour celsius))))
```

and then we perform the conversion

```clojure
(convert 43 watt-per-sq-meter-kelvin kcal-per-sq-foot-celsius-hour) ;; = 3.437235
```



# Conclusion

We presented a unit as a mathematical object and defined several operations that produce other
derived units. Equations
$\ref{relative.change.def}, \ref{multiplicative.change.def}, \ref{exponential.change.def}$
and $\ref{prefix.def}$ give us all the necessary tools to derive any kind of unit as long as
its conversion function is given by $\ref{conversion.fun.gen}$.
