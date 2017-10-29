# ساختار فایل ورودی \(pdf\) :

برای استفاده از کد باید یک فایل ورودی شامل اطلاعات مسئله از جمله  نوع محاسبات، تعداد و نوع اتم یا اتم های مورد استفاده، ساختار بلوری، فاصله‌ی اتم ها با یکدیگر، تعداد الکترون‌های لایه‌ی ظرفیت، باردار بودن یا نبودن ساختار مورد نظر، مکان و عدد اتمی عنصرهای مورد استفاده، تابع چگالی حاکم بر ماده و... تهیه شود.  
این فایل یک فایل متنی است که می‌تواند با استفاده از یک نرم افزار ویرایش فایل مانند wordpad  نوشته شود و با پسوند \(in.\) ذخیره می‌شود.  
هر فایل ورودی شامل قسمت هایی \(CONTROL، SYSTEM، ELECTRONS، ATOMIC\_SPECIES، ATOMIC\_POSITIONS، K\_POINTS و …\) است که هر قسمت با یک اسلش \(/\) از قسمت بعدی جدا شده است.

قسمت اول فایل ورودی  CONTROL است که می‌تواند شامل قسمت های زیر باشد:

```
calculation = 'scf' ,
restart_mode = 'from_scratch',
etot_conv_thr = 1.0E-6    , 
forc_conv_thr = 1.0D-6   ,
outdir='/root/Desktop/out/Graphenetest',
pseudo_dir = '/root/Desktop/ps', 
tprnfor   = .true.
tstress = .true
```

که calculation  مانند شکل 7 می‌تواند شامل scf، nscf  و ...باشد. ران scf پایه ای ترین ران و nscf ران غیر خود ساز گار است به این معنی که در یک حلقه محاسبات انجام می‌شود.

```
calculation

                     Default: 'scf'
a string describing the task to be performed:
  'scf',
  'nscf',
  'bands',
  'relax',
  'md',
  'vc-relax',
  'vc-md',

  (vc = variable-cell).
```

شکل 7 انواع محاسبات

به صورت پیش فرض  restart\_mode = 'from\_scratch' است، همانطور که می دانید DFT بر اساس چگالی بار کار می‌کند و  با یک حدس اولیه در حلقه‌ی محاسبات دقت را افزایش می دهد، اما اگر به هر دلیلی مانند قطع برق اجرای برنامه متوقف شد، اگر restart\_mode =restart' قرار دهید محاسبات را از آخرین چگالی بار بدست آمده شروع می‌کند.  
      etot\_conv\_thr = 1.0E-6 یعنی انرژی کل را تا چند رقم اعشار محاسبه کنید. در  outdir آدرس فایل خروجی را می دهیم که با پسوند out ذخیره می‌شود و شامل اطلاعاتی از جمله تابع موج ، چگالی بار و محاسبات می‌باشد ، همچنین  pseudo\_dir شامل آدرس شبه پتانسیل است.

قسمت دوم  SYSTEM  می‌تواند شامل بخش های زیر باشد و توضیحات جزییات آنها در شکل های 1تا 7 به تفصیل داده شده است.

```
SYSTEM
ibrav = 4,
celldm(1) = 4.6354 ,
celldm(3) = 7 ,
nbnd = 8,
nat = 2,
ntyp = 1,
ecutwfc = 30 ,
ecutrho = 300,
occupations = 'smearing' ,
degauss= 0.01 ,
smearing= 'gaussian',
```

که ibrav مشخص کننده نوع شبکه ی بلوری است، همانطور که میدانید ما 14 نوع ساختار بلوری داریم. برای مثال در شکل 8 پنج نمونه از آن را مشاهده می‌کنید. برای ibrav صفر، شما می‌توانید ساختار دلخواه خود را بسازید. برای ibrav=1 که به آن sc می گویند سلول واحد آن یک اتم دارد و هر اتم، 6 اتم در همسایگی خود دارد همچنین برای ibrav=3 که به bcc معروف است سلول واحد آن 2 اتم و در همسایگی هر اتم 8 اتم وجود دارد. در ibrav=2 که fcc نام دارد سلول واحد آن 4 اتم و در شبکه بلوری هر اتم، 8 اتم در اطراف خود دارد همچنین ibrav=4 ساختار هگزاگونال می‌باشد. در ادامه celldm ها را توضیح می دهیم، می دانیم هر سلول واحد با 6 پارامتر در فضا تعیین می‌شود با توجه به این  امر برای بردارهای این ساختار ها و زایه بین بردار های آن ها  از \(6-1\)celldm استفاده می کنیم.

```
ibrav    INTEGER
Status:    REQUIRED
  Bravais-lattice index. If ibrav /= 0, specify EITHER
  [ celldm(1)-celldm(6) ] OR [ A, B, C, cosAB, cosAC, cosBC ]
  but NOT both. The lattice parameter "alat" is set to
  alat = celldm(1) (in a.u.) or alat = A (in Angstrom);
  see below for the other parameters.
  For ibrav=0 specify the lattice vectors in CELL_PARAMETERS,
  optionally the lattice parameter alat = celldm(1) (in a.u.)
  or = A (in Angstrom), or else it is taken from CELL_PARAMETERS

ibrav      structure                   celldm(2)-celldm(6)
                                     or: b,c,cosab,cosac,cosbc
  0          free
      crystal axis provided in input: see card CELL_PARAMETERS

  1          cubic P (sc)
      v1 = a(1,0,0),  v2 = a(0,1,0),  v3 = a(0,0,1)

  2          cubic F (fcc)
      v1 = (a/2)(-1,0,1),  v2 = (a/2)(0,1,1), v3 = (a/2)(-1,1,0)

  3          cubic I (bcc)
      v1 = (a/2)(1,1,1),  v2 = (a/2)(-1,1,1),  v3 = (a/2)(-1,-1,1)

  4          Hexagonal and Trigonal P        celldm(3)=c/a
      v1 = a(1,0,0),  v2 = a(-1/2,sqrt(3)/2,0),  v3 = a(0,0,c/a)
      .
      .
      .
      .
```

```
                                                                                        شکل 8 نمونه ای از ibriv شبکه های بلوری
```

در واقع clledm ها بسته به نوع ساختار ها، طول بردار یا فاصله ی بین اتم های ساختار بلوری را مشخص می‌کنند. در شکل 9 بیان می‌کند که celldm\(1\)=a مقدار بردار a  و celldm\(2\)=b/a وcelldm\(3\)=c/a می‌باشد همچنین celldm\(4\)=cosα و celldm\(5\)=cosβ و celldm\(6\)=cos γ است.

```
celldm(i), i=1,6    REAL
See:    ibrav
Crystallographic constants - see the ibrav variable.
Specify either these OR A,B,C,cosAB,cosBC,cosAC NOT both.
Only needed values (depending on "ibrav") must be specified
alat = celldm(1) is the lattice parameter "a" (in BOHR)
If ibrav==0, only celldm(1) is used if present;
cell vectors are read from card CELL_PARAMETERS
Or:

A, B, C, cosAB, cosAC, cosBC    REAL
See:    ibrav
Traditional crystallographic constants:

  a,b,c in ANGSTROM
  cosAB = cosine of the angle between axis a and b (gamma)
  cosAC = cosine of the angle between axis a and c (beta)
  cosBC = cosine of the angle between axis b and c (alpha)

The axis are chosen according to the value of ibrav.
Specify either these OR celldm but NOT both.
Only needed values (depending on ibrav) must be specified.

The lattice parameter alat = A (in ANGSTROM ).

If ibrav == 0, only A is used if present, and
cell vectors are read from card CELL_PARAMETERS.
```

شکل 9 celldm ها و توضیحات آن ها

که nband بیانگر تعداد باند های اتم مورد نظر می‌باشد به عنوان مثال در این ساختار فقط یک نوع اتم کربن داریم ntyp آن برابر یک می‌باشد و چون دو اتم کربن داریم،nat برابر 2 و چون الکترون های لایه ظرفیت کربن 4 می‌باشد پس nbad=8 می‌شود.

```
nbnd    INTEGER
Default:    for an insulator, nbnd = number of valence bands (nbnd = # of electrons /2); 
for a metal, 20% more (minimum 4 more)
Number of electronic states (bands) to be calculated.
Note that in spin-polarized calculations the number of
k-point, not the number of bands per k-point, is doubled
```

شکل 10 توضیحات nband  
برای توضیحات بیشتر می‌توانید از فولدر Doc  استفاده کنید، که پس از باز کردن برنامه  vmware  مسیر زیر را مانند شکل 11 طی کنید. البته توجه داشته باشید که این مسیر بنا یه ورژن اسپرسو نصبی شما می‌تواند کمی تغییر کند.  
                                                                                                                    Vmware.  root.  softwares.  espresso5.  espresso5.1.2.  doc

@@@شکل 11مسیر فایل Doc جهت توضیحات کامل ساختار ورودی  
و همچنین میدانیم:

1bohr= 1 a.u.\(atomic unit\)=0.529177249 angstroms

1 Rydberg\(Ry\)=13.6056981 ev

1ev=1.60217733 @@@@ Joules

انرژی cutoff  انرژی سنتیک تابع موجی بر حسب ریدبرگ می‌باشد که باید همگرا شود. همچنین ecutrho ،میتواند 8  تا 10 برابر انرژی کات می‌باشد که برای شبه پتانسیل های ultrasoft استفاده می‌شود . برای شبه پتانسیل norm-conserving و PAW چهار برابر انرژی کات می‌باشد که نیاز به تایپ آن نیست بر حسب  قرار داد خودش چهار برابر در نظر می‌گیرد و توضیحات آن در شکل 13 داده شده است.

```
ecutwfc    REAL
Status:    REQUIRED
kinetic energy cutoff (Ry) for wavefunctions
```

شکل 12 انرژی کات

```
ecutrho    REAL
Default:    4 * ecutwfc
Kinetic energy cutoff (Ry) for charge density and potential
For norm-conserving pseudopotential you should stick to the
default value, you can reduce it by a little but it will
introduce noise especially on forces and stress.
If there are ultrasoft PP, a larger value than the default is
often desirable (ecutrho = 8 to 12 times ecutwfc, typically).
PAW datasets can often be used at 4*ecutwfc, but it depends
on the shape of augmentation charge: testing is mandatory.
The use of gradient-corrected functional, especially in cells
with vacuum, or for pseudopotential without non-linear core
correction, usually requires an higher values of ecutrho
to be accurately converged.
```

شکل 13 توضیحات ecutrho  
در قسمت بعد  با توجه به شکل 14 پارامتر occupations را داریم که برای فلزات یا رسانا ها smearing است که شامل دو پارامتر بعدی یعنی smearing و  deguss  نیز می‌باشد به طور مثال گرافن رساناست و در رساناها گاف انرژی وجود دارد و این گاف برای ما قابل تغییر و اهمیت است به دنبال آن دقت آن را با گزینه ای مانند degauss \(بر حسب ریدبرگ\) می‌توانیم بیشتر کنیم .  
occupations را برای نارسانا ها fixed در نظر می گیریم. توجه داشته باشید برای محاسبه  DOS در nscf،  occupations را tetrahedra می‌گذاریم.

```
occupations    CHARACTER
 Available options are:

'smearing' :
gaussian smearing for metals;
see variables smearing and degauss

'tetrahedra' :
Tetrahedron method, Bloechl's version:
P.E. Bloechl, PRB 49, 16223 (1994)
Requires uniform grid of k-points, to be
automatically generated (see card K_POINTS).
Well suited for calculation of DOS,
less so (because not variational) for
force/optimization/dynamics calculations.

'tetrahedra_lin' :
Original linear tetrahedron method.
To be used only as a reference;
the optimized tetrahedron method is more efficient.

'tetrahedra_opt' :
Optimized tetrahedron method:
see M. Kawamura, PRB 89, 094515 (2014).
Can be used for phonon calculations as well.

'fixed' :
for insulators with a gap

'from_input' :
The occupation are read from input file,
card OCCUPATIONS. Option valid only for a
single k-point, requires nbnd to be set
in input. Occupations should be consistent
with the value of tot_charge.
```

شکل 14 توضیحات occupations

و به همین ترتیب قسمت سوم ELECTRONS شامل بخش زیر است که به معنای استفاده از بخشی از اطلاعات چگالی بار حلقه ی قبلی  scf است.

ELECTRONS  
                  conv\_thr = 1.D-6 ,

```
conv_thr_multi    REAL
Default:    1.D-1
When adaptive_thr = .TRUE. the convergence threshold for
each scf cycle is given by:
max( conv_thr, conv_thr_multi * dexx )
```

شکل 15 توضیحات  
و قسمت چهارم ATOMIC\_SPECIES عدد اتمی و نوع پتانسیل عنصر مورد استفاده را مشخص می‌کند که در فایل ps  دخیره شده است و در بخش انواع پتانسیل ها که شامل \(norm-conserving، ultrasoft و PAW\) به آن اشاره خواهیم کرد.  
در قسنت C.pz-vbc.UPF حرف C نشان دهنده اتم کربن و PZ نوع تقریب را نشان می دهد که اگر PZ  باشد از تقریب LDA \(موادی با چگالی بار یکنواخت\) و اگر pbe باشد از تقریب GGA \(موادی با چگالی بار متفاوت\) استفاده کرده ایم. شبه پتانسیل ها  را با پسوند UPF ذخیره می‌کنیم و حروف قبلی نشان دهنده نام نویسنده می‌باشد.

ATOMIC\_SPECIES  
C    12.0107    C.pz-vbc.UPF  
C    12.0107    C.pbe.vbc.UPF

در قسسمت پنجم ATOMIC\_POSITIONS مختصات اتم های مورد نظر را مشخص می‌کنیم که می‌تواند بر حسب \( alat \| bohr \| angstrom \| crystal \| crystal\_sg\) باشد که اگر بر حسب alot یا  crystal باشد، زمانی که می خواهیم ریلکس کنیم، فقط کافی است تغییرات را روی\( celldm 1\) انجام دهیم. در ادامه فصل  بخش1.5 به توضیح ریلکس پرداخته شده است.

ATOMIC\_POSITIONS \(angstrom\)  
C        0.000000000   0  0  
C        0.000000000   1.418135710  0

در انتها قسمت K\_POINTS است  که می‌تواند بر حسب tpiba \| automatic \| crystal \| gamma\) \( fhan tpiba\_b \| crystal\_b \| tpiba\_c \| crystal\_c باشد. از tpiba در محاسبات بند استراکچر بخش 1.8 استفاده می‌کنیم. در واقع نقاط در فضای حقیقی با تبدیلی به فضای وارون تبدیل می‌شوند  \(ضریبa /2π\) و هر سلول واحد در فضای حقیقی با سه بردار a1،a2  و a3 مشخص می‌شود که اگر نقطه ای در این فضا نسبت به دستگاه مختصات کارتزین سنجیده شود از واحد \(angstrom\) استفاده می‌کنیم و اگر نقطه مذکور نسبت به بردار های a1،a2  و a3 سنجیده شود از واحد \( \(crystal\) استفاده می‌کنیم. همچنین چین شرایطی در فضای وارون نیز وجود دارد که اگر نقطه ای در فضای وارون نسبت به دستگاه مختصات کارتزین باشد واحد آن tpiba و اگر نسبت به بردار های b1,b2 و b3 که بردار های سلول واحد در این فضا هستند گزارش شود از واحد \( \(crystal\) استفاده می‌کنیم. سه رقم آخر مختصات شروع kpoint هاست که می‌تواند 1 1 1 نیز باشد که به معنای شیفت شروع این نقطه هاست. با این شیفت ها می‌توان ماتریسی را که قطری نیست، قطری کرد که روابط بهتر محاسبه شود. همچنین اگر کاپوینت در حالت gamma  باشد k=0 \(بردار موج 0 0 0\)است و برای مطالعه روی مولکول ها کاربرد دارد.  
Kpoint ها می‌توانند یک، دو و یا سه بعدی باشند که طرز نوشتن هر یک در قسمت زیر توضیح داده شده است:

K\_POINTS {automatic}  
 1 1 6 0 0 0   یک بعدی  
6 6 1 0 0 0    دو بعدی  
6 6 6 0 0 0    سه بعدی

برای درک بهتر به توضیح مختصری از مفاهیم می پردازیم توجه داشته باشید که این تمثیل ها فقط برای درک بهتر و ارتباط برقرار کردن با فضای مجازی می‌باشد و نگرش شخصی است. کاپوینت ها تعدای نقاط در فضای وارون می‌باشند که ما برای اجرای صحیح برنامه و افزایش سرعت اجرا به تعداد مشخص شده ای از آن ها نیاز داریم اگر این تعداد کم باشد قسمتی از نقاط فضای وارون را از دست داده ایم و اگر زیاد باشد حجم محاسبات افزایش پیدا می‌کند. برای مشخص کردن تعداد کاپوینت از ecutwfe استفاده  می‌کنیم که در واقع شعاع دایره ای به  شکل 16 است که کاپوینت ها در آن محدوده، لازم و کافی برای محاسبات هستند، مانند جعبه ای که توپ های بیلیارد در آن جای می گیرند. اما اعدادی که برای کاپوینت و ecut  به برنامه می دهیم شانسی نیست و با استفاده از محاسبات بدست آمده است. هر چه شبکه حقیقی  بزرگتر باشد فضای وارون آن کوچکتر است.

@@@@@@@شکل 16 نمایی از شعاع دایره که بیانگر انرژی کات می‌باشد.  
لازم به ذکر است که فایل ورودی بنا به استفاده می‌تواند شامل  قسمت های دیگر نیز باشد اما ما در اینجا به بخش هایی پرداختیم که بیشتر کاربرد دارد. در انتها نیز در شکل 17یک فایل ورودی آماده را مشاهده می‌کنید:

```
 &control
    calculation = 'scf',
    verbosity = 'high'
    prefix = 'Al_exc2'
    outdir = './tmp',
    pseudo_dir = './pseudo',
 /
 &system
    ibrav =  2, 
    celldm(1) = 7.65, 
    nat =  1, 
    ntyp = 1,
    ecutwfc = 18.0,
    occupations = 'smearing',
    smearing = 'marzari-vanderbilt',
    degauss = 0.05,
 /
 &electrons
    mixing_beta = 0.7,
 /

ATOMIC_SPECIES
 Al 26.98  Al.pz-vbc.UPF

ATOMIC_POSITIONS (alat)
 Al 0.0 0.0 0.0

K_POINTS (automatic)
  6 6 6 1 1 1
```

شکل 17 نمونه ای از فایل ورودی  
توجه کنید که در هر مرحله از ورودی می‌توانید با مراجعه به فایل INPUT\_PW  که در فایل doc  قرار دارد اطلاعات کافی را بدست آورید این فایل به صورت pdf و html در فولدر doc  قرار داده شده است.

