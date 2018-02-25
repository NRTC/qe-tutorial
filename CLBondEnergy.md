## بدست آوردن انرژی پیوندی کلر

در گام اول یک مولکول کلر در نظر می گیریم و چون مولکول است، کاپوینت را برابر گاما قرار می‌دهیم سپس برای بدست آوردن انرژی مینیمم یک اتم را ثابت گرفته و مکان اتم دوم را به تکرار جابجا می‌کنیم و بر اساس انرژی کل در خروجی نمودار رسم می‌کنیم، مکان اتم دوم در انرژی مینیمم برای ما حائز اهمیت می‌باشد.

```
$ more c12.1n

&CONTROL
calculation = 'scf' ,
prefix = 'c12' ,
outdir='/root/Desktop/out',
pseudo_dir = './root/Desktop/ps',

&SYSTEM
ibrav = 1,
celldm(1)=20.0 ,
nat = 2,
ntyp = 1,
ecutwfc =100 ,
/
&ELECTRONS
conv_thr = 1.0D-8 ,
/
ATOMIC_SPECIES
Cl 1.0 cl.pz-bhs.upf
ATOMIC_POSITIONS bohr
Cl 0.00 0.00 0.00
Cl 0.00 0.00 0.00
K_POINTS {gamma}
```

شکل 35 ورودی مولکول کلر

$$E_{{cl}_2} = -59.99059545 Ry$$

![](/assets/36.png)

شکل 36 نمودار انرژی بر حسب مکان مولکول  کلر

در گام بعدی انرژی کل را برای یک اتم کلر در نظر میگیریم\( شکل 37\).

```
$ more c12.1n

&CONTROL
calculation = 'scf' ,
prefix = 'c12' ,
outdir='/root/Desktop/out',
pseudo_dir = './root/Desktop/ps',

&SYSTEM
ibrav = 1,
celldm(1)=20.0 ,
nat = 1,
ntyp = 1,
ecutwfc =100 ,
nspin = 2,
tot_magnetization = 1.0,
occupations = 'smearing',
degauss = 0.001,
/
&ELECTRONS
conv_thr = 1.0D-8 ,
/
ATOMIC_SPECIES
Cl 1.0 cl.pz-bhs.UPF
ATOMIC_POSITIONS
Cl 0.00 0.00 0.00
K_POINTS gamma
```

شکل 37 ورودی اتم کلر

$$E_{cl} = -29.86386108 Ry$$

و با استفاده از فرمول زیر انرژی پیوندی کلر را می‌توان محاسبه کرد.

$$E_{diss} = E_{cl_2} - 2E_{cl}$$

$$E_{diss} = 0.262873 Ry = 3.58 eV$$

