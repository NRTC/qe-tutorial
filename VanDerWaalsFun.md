## تابع واندروالس

همانطور که می دانید ما دو نوع جذب فیزیکی و شیمیایی داریم که جذب فیزیکی نوعی فرایند جذب است که در آن نیروهای مؤثر، نیروهای بین‌مولکولی \(واندروالس\) بوده و در اثر این فرایند جذب، تغییر محسوسی درالگوی اوربیتال الکترونی اتم‌های درگیر به وجود نمی‌آید. این نوع جذب دارای انرژی فعال‌سازی نیست و انرژی آزاد شده در طی آن در مقایسه با جذب شیمیایی کمتر است.

برای اجرای نمونه واندروالس، شما باید این روش را دنبال کنید:  
در ابتدای کار برای اجرای شبیه سازی این نوع خاص از اجرا -VDW-DF - نیاز به تولید"vdW\_kernel\_table"، در فایل شبه پتانسیل است که یک بار تولید و در تمام محاسبات از آن استفاده می‌کنند. برای تولید vdW\_kernel\_table کافی است فایل generate-vdw-kemel را مطابق شکل 82 به فایل شبه پتانسیل برده و در آنجا مطابق شکل 83 اجرا کنیم.

![](/assets/82222.png)

شکل 82 مسیر تولید  vdW\_kernel\_table

![](/assets/83.png)

شکل 83 دستور تولید vdW\_kernel\_table در ترمینال

2- گام بعدی  ویرایش "environment\_variables" از فایل اصلی دایرکتوری اسپرسو، اضافه کردن  input-dft  مطابق شکل 84 در قسمت سیستم  برنامه است. توجه داشته باشید کلیه input  هایی که می‌توانید استفاده کنید درفایل  funct-f90 مطابق شکل 85 قرار دارد و استفاده از شبه پتانسیل GGA مناسب تر است.

```
&SYSTEM
                    ibrav = 4
                    ceiidm(1)=4.6304,
                    celldm(3)=7,
                    nbnd=8,
                    nat=2,
                    ntyp=1,
                    ecutwfc=55,
                    ecutrho=550,
                    occupations='smearing',
                    degauss=0.01,
                    smearing='gaussian',
                    input_dft='vdw-df2-b86r',
```

شکل 84 ویرایش ورودی  واندروالس

![](/assets/8500.png)

شکل 85 مسیر فایل  funct-f90  
اگر به مثال های بیشتری نیاز داشتید می‌توانید از مثال های خود اسپرسو از vdw-df-example مطابق شکل 86 استفاده کنید.

![](/assets/85.png)

شکل 86 مثال های اجرایی واندروالس

**خروجی واندر والس**  
در خروجی برنامه به سه خط توجه ویژه نمایید.  
1- مطابق شکل 87 ، چاپ خط 21 باید لحاظ شود.  
2- مطابق شکل 88،  total energr , xc  و برخی دیگر  از پارامتر ها نسبت به حالتی که واندروالس ندارد باید تغییر کند.

```
15    Current dimensions of program PWSCF are:
16     Max number of different atomic species (ntypx) = 10
17     Max number of k-points (npk) =  40000
18     Max angular momentum in pseudopotentials (lmaxx) =  3
19
20     IMPORTANT: XC functional enforced from input :
21     Exchange-correlation      = VDW-DF2-B86R ( 1  4 26  0 2 0 )
22     Any further DFT definition will be discarded
23     Please, verify this is what you really want
```

شکل 87 قسمتی از خروجی واندروالس

```
358!    total energy              =     -22.53912642 Ry
359     Harris-Foulkes estimate   =     -22.53912596 Ry
360     estimated scf accuracy    <       0.00000052 Ry
361
362     The total energy is the sum of the following terms:
363
364     one-electron contribution =    -187.82227925 Ry
365     hartree contribution      =      95.07064481 Ry
366     xc contribution           =      -6.91958108 Ry
367     ewald contribution        =      77.13271098 Ry
368     smearing contrib. (-TS)   =      -0.00062188 Ry
```

شکل 88 انرژی کل خروجی واندر والس

