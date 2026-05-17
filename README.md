

# Analytical model

## ✨ Info
- **Analytical model** available in code file `analytical.py`
- **Analytical Determination of input impedance of half-wave dipole in free space and half-space**
- **Code diagrams** for visual understanding of input data and output files
- **LaTeX equations used in code** for scientific notation
- **Good luck, Author: Josip Salinovic** 
#
```mermaid
flowchart TD
    A[Start] --> B[Input Parameters]

    B --> B1[Dipole Length]
    B --> B2[Dipole Radius]
    B --> B3[Half-space or Free space Medium Properties (permitivity and conductivity)]
    B --> B4[Height Above Halfspace]
    B --> B5[Frequency Range in Hz]

    B1 --> C[Initialize Electromagnetic Model]
    B2 --> C
    B3 --> C
    B4 --> C
    B5 --> C

    C --> D[Generate Frequency Sweep]

    D --> F[For Each Frequency]
    
    F --> G[Calculate average complex Fresnel reflection coefficient ]
   
    G --> H[Calculate sine and cosine integral using Gauss-Legendre quadrature]
     --> H[Calculate Impedance from analytic formula]

    H --> I{More Frequencies?}
    I -->|Yes| F
    I -->|No| J[Store Impedance Results]

    J --> K[Generate Output Text File]
    K --> L[Impedance.txt Contains Frequency in MHz vs Input Impedance in Ohm]

    L --> M[End]
```
# Equations

$$
    Z_{\text{in}}^{H}
    =
    Z_{\text{in}}^{F}
    +
    \left\langle r_{\mathrm{TM}} \right\rangle
    \frac{I_{0}}{I_{g}^{2}}
    \int_{-\frac{l}{2}}^{\frac{l}{2}}
    \sin\!\left[
    k\left(
    \frac{l}{2} - \left| z' \right|
    \right)
    \right]
    E_{z}(2h, z')
    \, dz'
    $$

$$
	Z_{\text{in}}^{\text{H}}= \frac{I_0^2(R^F+\braket{r_{TM}}R^{\text{H}})}{I_g^2(z'\!=\!0)}=\frac{\cancel{I_0^2}(R^F+\braket{r_{TM}}R^{\text{H}})}{\cancel{I_0^2}\sin^2(kl/2)}=(R^{F}+\braket{r_{TM}}R^{\text{H}})\csc^2(kl/2),
$$
where free space resistance is
$$
\begin{aligned}
R^{\text{F}}=\!\frac{\eta}{2\pi}\Biggl\{\! \gamma\!+\!\ln(kl)\!-\!\operatorname{Ci}(kl)\!+\!\frac{\sin(kl)}{2} \left[ \operatorname{Si}(2kl)\! -\!2\operatorname{Si}(kl)\right] \\
+ \frac{\cos(kl)}{2}\left[ \gamma+\ln\!\left( \frac{kl}{2}\right) +\operatorname{Ci}(2kl)-2\operatorname{Ci}(kl)\right]\Biggr\}
\end{aligned}
$$
and free space reactance is
$$
\begin{aligned}
X^{\text{F}}=\frac{\eta}{4\pi} \Bigg\{ 2\operatorname{Si}(kl)+\cos(kl)\left[ 2\operatorname{Si}(kl) -\operatorname{Si}(2kl)\right] \\
- \sin(kl)\left[ 2\operatorname{Ci}(kl)-\operatorname{Ci}(2kl)-\operatorname{Ci}\left( \frac{2ka^2}{l} \right) \right] \Biggr\}
\end{aligned}
$$.
Half-space resistance and reactance are
$$
\begin{aligned}
&R^{\text{H}} =\frac{\eta}{4\pi} \Biggl\{
-2\operatorname{Ci}(k \rho)
+\operatorname{Ci}\!\left(k\frac{A - l}{2}\right)
+\operatorname{Ci}\!\left(k\frac{A + l}{2}\right) \\
&-\sin(kl)\Bigl[
\operatorname{Si}\!\left(k(B + l)\right)
-\operatorname{Si}\!\left(k(B - l)\right)
-\operatorname{Si}\!\left(k\frac{A + l}{2}\right) \\
&\qquad
+\operatorname{Si}\!\left(k\frac{A - l}{2}\right)
\Bigr]
-\cos(kl)\Bigl[
\operatorname{Ci}\!\left(k(B + l)\right)
+\operatorname{Ci}\!\left(k(B - l)\right) \\
&\qquad
-\operatorname{Ci}\!\left(k\frac{A + l}{2}\right)
-\operatorname{Ci}\!\left(k\frac{A - l}{2}\right)
\Bigr] \\
&+2\cos\!\left(\tfrac{kl}{2}\right)\sin\!\left(\tfrac{kl}{2}\right)
\Bigl[
\operatorname{Si}\!\left(k\left(C + \dfrac{l}{2}\right)\right)
-\operatorname{Si}\!\left(k\left(C - \dfrac{l}{2}\right)\right)
\Bigr] \\
&+2\cos^2\!\left(\tfrac{kl}{2}\right)
\Bigl[
\operatorname{Ci}\!\left(k\left(C + \dfrac{l}{2}\right)\right)
+\operatorname{Ci}\!\left(k\left(C - \dfrac{l}{2}\right)\right)
-2\,\operatorname{Ci}(k\rho)
\Bigr]
\Biggr\}
\end{aligned}
$$
and
$$
\begin{aligned}
&X^{\text{H}} = \frac{\eta}{4\pi}\Biggl\{
-\operatorname{Si}\!\left(k\frac{A - l}{2}\right)
-\operatorname{Si}\!\left(k\frac{A + l}{2}\right)
+2\operatorname{Si}(k\rho) \\
&-\cos(kl)\Bigl[
\operatorname{Si}\!\left(k\frac{A - l}{2}\right)
+\operatorname{Si}\!\left(k\frac{A + l}{2}\right)
-\operatorname{Si}(B - l)
-\operatorname{Si}(B + l)
\Bigr] \\
&-\sin(kl)\Bigl[
\operatorname{Ci}\!\left(k\frac{A - l}{2}\right)
-\operatorname{Ci}\!\left(k\frac{A + l}{2}\right)
-\operatorname{Ci}(B - l)
+\operatorname{Ci}(B + l)
\Bigr] \\
&+2\cos\!\left(\tfrac{kl}{2}\right)\sin\!\left(\tfrac{kl}{2}\right)
\Bigl[
\operatorname{Ci}\!\left(k\left(C + \dfrac{l}{2}\right)\right)
-\operatorname{Ci}\!\left(k\left(C - \dfrac{l}{2}\right)\right)
\Bigr] \\
&+2\cos^2\!\left(\tfrac{kl}{2}\right)
\Bigl[
-\operatorname{Si}\!\left(k\left(C + \dfrac{l}{2}\right)\right)
-\operatorname{Si}\!\left(k\left(C - \dfrac{l}{2}\right)\right)
+2\operatorname{Si}(k\rho)
\Bigr]
\Biggr\}
\end{aligned}
$$.