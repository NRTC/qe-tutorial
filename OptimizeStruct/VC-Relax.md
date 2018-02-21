# Vc-relax

در این مرحله نیز مانند ریلکس، ساختار را بهینه می‌کنیم با این تفاوت که کاری که در حالت قبل به صورت دستی انجام دادیم در این حالت، سیستم به طور اتومات انجام میدهد و در انتها به ما اطلاعات atomic position و پارامتر شبکه \(celldm\) را در خروجی می دهد. در مرحله قبل ریلکس برای گرافن دو کربنه انجام شد در اینجا ورودی        vc-relax برای گرافیت 4 کربنه ویرایش شده است. در فایل خروجی بردار شبکه از پارامتر شبکه سلول های اصلی در ورودی بدست می اید.

```
 &CONTROL
           calculation = 'vc-relax' ,
           prefix = 'graphite',
           outdir='./',
           pseudo_dir = './', 
/
 &SYSTEM
           ibrav = 4,
           celldm(1)=4.0,
           celldm(3)=2.0,
           nat = 4,
           ntyp = 1,
           ecutwfc = 100 ,
/
 &ELECTRONS
           conv_thr = 1.0d-8 ,
/
&IONS
/
&CELL
/
ATOMIC_SPECIES
C    12.0107     C.pz-vdc.UPF
ATOMIC_POSITIONS (crystal)
c 0.00 0.00 0.25
c 0.00 0.00 0.75
c 0.3333 0.6666 0.25
c 0.6666 0.3333 0.75
K_POINTS {automatic}
6  6  2   1  1  1
```

شکل 33 ورودی vc-relax

```
Begin final coordinates
   new unit-cell volume = 200.62641 a.u.^3 (   29.72977 Ang^3)

CELL_PARAMETERS (alat= 4.000000000)
 1.149452048  0.000000000  0.000000000
-0.574726024  0.995454674  0.000000000
 0.000000000  0.000000000  2.739654388

ATOMIC_POSITIONS (crystal)
c    0.000000000 0.000000000 0.250000000
c    0.000000000 0.000000000 0.750000000
c    0.333333000 0.666666000 0.250000000
c    0.666666000 0.333333000 0.750000000
End final coordinates
```

شکل 34 خروجی vc-relax

