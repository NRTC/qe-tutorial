## ‫بررسی اتم ‪Fe‬‬

گرچه DFT + U برای آهن بالک بسیار مفید نیست ، ما از این سیستم برای آشنا شدن با محاسبات هابارد   Uاستفاده می‌کنیم.  
به طور مقدماتی شما می‌توانید اثر U را روی بالک آهن بررسی کنید فقط با استفاده از مقایسه نتایجی \( به عنوان مثال DOS\) که از DFT و DFT + U   بدست می آورید . برای این منظور شما می‌توانید از اسکریپت های run\_Fe\_NOU و run\_Fe\_U استفاده کنید .

### محاسبه scf

بیایید اسکریپت scf رابررسی کنیم . بخش اصلی فایل ورودی برای محاسبه SCF به شرح زیر است :

```
&system
ibrav= 1, 
celldm(1)=5.42, 
nat= 2, 
ntyp= 2,
ecutwfc = 30.0, 
ecutrho = 360.0,
occupations='smearing',   smearing='mp',   degauss=0.01,
nbnd = 14,
nspin=2,
starting_magnetization(1)= 0.6
starting_magnetization(2)= 0.6
lda_plus_u = .true.
Hubbard_U(1)= 1.d-20
Hubbard_U(2)= 1.d-20
/
&electrons
mixing_beta = 0.7
conv_thr = 1.0d-9,
/
ATOMIC_SPECIES
Fe1   1. Fe.pbe-nd-rrkjus.UPF
Fe     1. Fe.pbe-nd-rrkjus.UPF
ATOMIC_POSITIONS crystal
Fe1 0.0 0.0 0.0
Fe 0.5 0.5 0.5
```

توجه کنید که این یک محاسبه DFT + U  با \( lda\_plus\_u = .true \) با در نظر گرفتن U بسیار کوچک است . ازآنجاکه توضیحات اولیه این U کوچک هیچ تاثیری روی نتایج ندارد ولی ضروری است کد قابل چاپ ماتریسهای occupation را داشته باشیم، نیاز خواهیم داشت پاسخ سیستم به اختلال بیرونی را بسنجیم .  
این مهم است که توجه داشته باشید که دو اتم در سلول واحد در انواع مختلف توصیف می‌شود :  
  \(fe , fe1\)این تفاوت را در قسمت شبه پتانسیلها وارد می‌کنیم. در واقع یکی از آنها موضوع پتانسیل اختلالی خواهد بود \(fe1\) \( اگر ما آنها را به عنوان نوع یکسان توصیف کنیم اختلال به هردو اضافه خواهد شد\). به طور کلی اتمی که در آن اختلال است به عنوان نوع متفاوت از دیگران نیاز به توصیف دارد. \(حتی باوجود شبه پتانسیل یکسان \)  
پس از آنکه اجرای SCF کامل شد برای شروع محاسبه اختلال آماده ایم .  
در فایل خروجی scf به مقدار عددی ethr در آخرین iteration نگاه کنید .

```
1957
1958     iteration # 12     ecut=    30.00 Ry     beta=0.70
1959     Davidson diagonalization with overlap
1960     ethr = 1.02E-11,   avg # of iteration = 4.0
```

شکل 133 خروجی scf

سپس عدد مربوط به آن را در قسمت electrons& مقابل diago\_thr\_init قرار می‌دهیم.

```
21  &electrons
22     startingpot = 'file'
23     startingwfc = 'file'
24     diagno_thr_int = 1.02E-11
25     mixing_beta = 0.7
26     conv_thr = 1.0d-9,
```

شکل 134 قسمتی از ورودی جدید scf  
همچنین پارامتر جدید Hubbard\_alpha را در محاسبات وارد کرده و برای آن مقادیر متفاوت alpha را به ازای  0.0 , -0.05 , 0.05 , -0.1 , 0.1 قرار می‌دهیم.  
این یک سری از مقادیر آلفا اطراف صفر است .  این آلفا تنها برای اتم 1 در نظر گرفته می‌شود.

```
13    nspin=2, 
14    starting_magnetization(1)= 0.6,
15    starting_magnetization(2)= 0.6,
16    lda_plus_u = .true.
17    Hubbard_U(1)= 1.d-20,
18    Hubbard_U(2)= 1.d-20,
19    Hubbard_alpha(1)= &alpha
20  /
```

شکل 135 قسمتی از ورودی جدید scf

برنامه را به ازای آلفاهای مختلف اجرا می‌کنیم در نتیجه خروجی‌های مختلف حاصل می‌شود.  
پس از نوشتن و اجرای صحیح محاسبات به نتایجی از فایلهای خروجی نیازمندیم که این نتایج شامل مقدار عددی \(Tr\[ns\(na\)\]  \(up, down, total \) برای تعداد اتمهای موجود به ازای هر کدام از مقادیر Hubbard\_alpha که به صورت جداگانه ران کردیم، می‌باشد.

البته لازم به ذکر است که این اطلاعات را از iteraction \#1 و End of self-consistent calculation استخراج می‌کنیم.  
سپس آنها را در فایل های زیر دسته بندی می‌کنیم.

```
1. dn0.at1.da.at2.dat
2. dn.at1.da.at2.dat
```

این مقادیر را برای فایل های حالت 1 از iteraction \#1  به صورت زیر حاصل می‌شود:

```
946     iteration #  1     ecut=    30.00 Ry     beta=0.70
947     Davidson diagonalization with overlap
948     c_bands:  1 eigenvalues not converged
949     ethr =  1.02E-11,  avg # of iterations =  6.1
950  --- enter write_ns ---
951  LDA+U parameters:
952 U( 1)     =  0.00000000
953 alpha( 1) =  0.10000000
954 U( 2)     =  0.00000000
955 alpha( 2) =  0.00000000
956 atom    1   Tr[ns(na)] (up, down, total) =   4.87293  2.58904  7.46197
```

شکل 136  iteration 1 فایل خروجی scf  
و برای فایل های حالت 2 از End of self-consistent calculation به صورت زیر حاصل می‌شود :

```
1380    End of self-consistent calculation
1381  --- enter write_ns ---
1382  LDA+U parameters:
1383 U( 1)     =  0.00000000
1384 alpha( 1) =  0.15000000
1385 U( 2)     =  0.00000000
1386 alpha( 2) =  0.00000000
1387 U( 3)     =  0.00000000
1388 alpha( 3) =  0.00000000
1389 U( 4)     =  0.00000000
1390 alpha( 4) =  0.00000000
1391 atom    1   Tr[ns(na)] (up, down, total) =   4.96187  3.71279  8.67466
```

شکل 137 End of self-consistent calculation فایل خروجی scf

بدیهی است از آنجا که دو اتم با یکدیگر معادل هستند ، به مختل کردن آنها را به طور جداگانه نیاز نداریم.  
پس از آنکه سری کامل محاسبات تمام شد برای محاسبه U آماده می‌شویم.

### بررسی اسکریپت ....\_...\_ grepnalfa_..._...

صدور فرمان “./grepnalfa\_sc1\_pbe”. این اسکریپت تمامی occupation ها را برای همه اتم ها از خروجی اجرای اختلال جمع آوری می‌کند و آنها را در فایل های dn.at1.da.at2.dat مینویسد . که در آن at1 مربوط به پاسخی است که اندازه گیری می‌کنیم ، at2 اتمی که در آن اختلال به کار گرفته شده است.  
اسکریپ  grepnalfa\_sc1\_pbe همچنین فایل file\_sc1  که با نام فایل dn\*.dat جمع آوری می‌شود را ایجاد می‌کند. برای اجرای آن اسکریپت grepnalfa\_sc1\_pbe را داخل برنامه قرار می‌دهیم سپس به ویرایش مربوط به نام خروجی‌های برنامه با آلفاهای مختلف می‌پردازیم :

     8 for con in -0.1 -0.05 0.0 0.05 0.1 
     9 do
    10
    11 sum1=`grep 'Tr' fe_sc1_$con.scf.out |tail -2 | awk '{if(NR==1) print $10}'`
    12 echo ' ' $con ' ' $sum1 >> dn_1_da_1.dat
    13 sum1=`grep 'Tr' fe_sc1_$con.scf.out |tail -2 | awk '{if(NR==2) print $10}'`
    14 echo ' ' $con ' ' $sum1 >> dn_2_da_1.dat
    15
    16 sum1=`grep 'Tr' fe_sc1_$con.scf.out |head -4 |tail -2 | awk '{if(NR==1) print $10}'`
    17 echo ' ' $con ' ' $sum1 >> dn0_1_da_1.dat
    18 sum1=`grep 'Tr' fe_sc1_$con.scf.out |head -4 |tail -2 | awk '{if(NR==2) print $10}'`
    19 echo ' ' $con ' ' $sum1 >> dn0_2_da_1.dat
    20
    21 done
    22
    23 echo ' dn_1_da_1.dat  dn0_1_da_1.dat' >> file_sc1
    24 echo ' dn_2_da_1.dat  dn0_2_da_1.dat' >> file_sc1
    25

شکل 138 اسکریپت grepnalfa\_sc1\_pbe  
پس از تکمیل آن را با دستور زیر اجرا می‌کنیم :

![](/assets/139.png)

شکل 139 ران اسکریپت grepnalfa\_sc1\_pbe

با استفاده از xmgrace می‌توان فایل dn.at1.da.at2.dat و فایل متناظر  dn0.at1.da.at2.dat را رسم کنید.  
شما باید رفتار خطی آلفای n wrt برای هر دو مورد مشاهده کنید. همچنین دو خط در آلفا = 0 با یگدیگر متفاوتند .کد محاسبه ماتریس پاسخ و برگردانی آنها از resp\_mat.f90 است.

### تولید فایلr.x

برای اجرای مراحل بعدی و محاسبه نهایی u نیاز به فایل r.x داریم. برای تولید فایل r.x به دو فایل comp\_resp\_mat.j و resp\_mat.f90 نیاز داریم.  
فایل comp\_resp\_mat.j به صورت زیر است:

![](/assets/140.png)

شکل 140 فایل comp\_resp\_mat.j  
در نتیجه در ترمینال داریم :

![](/assets/141.png)

شکل 141 ترمینال فایل comp\_resp\_mat.j  
پس از ران این قسمت فایل r.x   تولید می‌شود:

![](/assets/142.png)

شکل 142 تولید r.x

### اجرای resp\_mat

پس از تولید فایل r.x می‌توان فایل resp\_mat.in را اجرا کرد.  
فایل ورودی resp\_mat.in به شرح زیر ساخته می‌شود:

&input\_mat

تعداد انواع اتمها \(اتمهایی که برای محاسبه u به‌کار می‌روند\)                                                                                                                                    ntyp = 1

تعداداتمهای هر نوع                                                                                                                                                                                      na\(1\) = 2

تعداد اختلال \(آلفا\)                                                                                                                                                                                        nalfa = 5

Magn =.true.

تنها زمانی استفاده می‌شود که دواتم در یک موقعیت کریستالوگرافی برابر با مغناطش مختلف باشند، زمانیکه چنین شرایطی را داشته باشیم می‌توان این پارامتر را حذف کرد یا از گزینه .fals. استفاده کرد. که در اینجا چون این شرایط را نداریم می‌توان این گزینه را حذف کرد.

فایل شامل موقعیتهای اتمی و بردارهای سلول واحد                                                                                                                                filepos = 'pos\_sc1'

توجه کنید که درفایل 'pos\_sc1' در مقابل موقعیتهای اتمی اعداد مربوط به مغناطش اتمها را نیز وارد کنیم، به این طریق که برای مغناطش مثبت مقدار 1+ ، مغناطش منفی مقدار 1- و برای اتمهایی که بدون مغناطش هستند مقدار 0 را قرار می‌دهیم .

برای افزودن یک "پس زمینه" خنثی .                                                                                                                                                      back = 'neutral'

فایل شامل اسامی فایل های dn\*dat                                                                                                                                                filednda = 'file\_sc1'

n1 = 4

تعداد سلولهای واحد در هر جهت برای ساخت ابرسلول                                                                                                                                                n2 = 4

برون یابی \( در این حالت یک ابرسلول 4x4x4 SC آن \)                                                                                                                                           n3 = 4

&end

برای اجرای این مرحله نیاز به ران توسط فرمان زیرداریم

./r.x &lt; resp\_mat.in&gt; resp\_mat.out

فرمان “./r.x &lt; resp\_mat.in”. فایل Umat.out محتویات ماتریس خطی را ایجاد می‌کند و تفاوت بین معکوسشان  U را تعیین می‌کند . در فایل Umat.out جستجو کنید برای مقادیر زیر :  
Number of atom ,  U1

### اجرای اسکریپت ucalc\_sc1\_pbe.j

اسکریپت  ucalc\_sc1\_pbe.j همه عملیات لازم برای محاسبه U را به طورخودکار انجام می‌دهد. در این اسکریپت دقت کنید کنید که ابتدا اطلاعات از فایل resp\_mat0.in فراخوانی ‌شده، سپس داخل فایل resp\_mat.in قرار داده می‌شود و برای یک حلقه به ازای n1,n2,n3 های مختلف این محاسبات تکرار می‌شود.

    if [ ! -f r.x ]; then
       ./comp_resp_mat.j
    fi

    rm dn*dat
    ./grepnalfa_sc1_pbe

    echo " &input_mat "> resp_mat0.in
    echo "   ntyp = 1 ">> resp_mat0.in
    echo "   na(1) = 2 ">> resp_mat0.in
    echo "   nalfa = 5 ">> resp_mat0.in
    echo "   filepos = 'pos_sc1' ">> resp_mat0.in
    echo "   back = 'no' ">> resp_mat0.in
    echo "   filednda = 'file_sc1' ">> resp_mat0.in

    rm -f Usc1_pbe.out
    for n1 in 1 2 3 4 5 6
    do

    rm -f resp_mat.in
    cp resp_mat0.in resp_mat.in

    echo "   n1 = $n1 ">> resp_mat.in
    echo "   n2 = $n1 ">> resp_mat.in
    echo "   n3 = $n1 ">> resp_mat.in
    echo " &end ">> resp_mat.in

    ./r.x < resp_mat.in
    nat=`grep 'number of atoms' Umat.out |tail -1|awk '{print $9}'`
    U=`grep U1 Umat.out |awk '{print $5}'`
    echo $nat $U >> Usc1_pbe.out
    done
    mv Umat.out Umat_sc1_pbe.$n1.$n1.$n1.out

شکل 143 اسکریپت  ucalc\_sc1\_pbe.j  
کل روش هم اکنون می‌تواند با شروع محاسبات در ابرسلول بزرگتر تکرار شود.  
برگردید به فهرست منشا و مجددا اجرای run\_Fe\_bcc8\_ucalc\_pbe را شروع کنید که محاسبات اختلالی روی ابرسلول  BCC 2x2x2 با 8 اتم را انجام می‌دهد. انواع و موقعیت اتم ها به صورت زیر است :

```
25 ATOMIC_SPECIES
26 Fe1 55.85  Fe.pz-nd-rrkjus.UPF
27 Fe  55.85  Fe.pz-nd-rrkjus.UPF
28 ATOMIC_POSITIONS {crystal}
29 Fe1  0.00000   0.00000   0.00000
30 Fe   0.50000   0.00000   0.00000
31 Fe   0.00000   0.50000   0.00000
32 Fe   0.00000   0.00000   0.50000
33 Fe   0.50000   0.50000   0.00000
34 Fe   0.00000   0.50000   0.50000
35 Fe   0.50000   0.00000   0.50000
36 Fe   0.50000   0.50000   0.50000
```

شکل 144 قسمتی از فایل ورودی Fe\_bcc8\_ucalc\_pbe

لطفا توجه کنید اتمی که در آن آلفا استفاده شده است همیشه به عنوان نوعی متفاوت از دیگران توصیف می‌شود هرچند با PP یکسان و همیشه در مبدا \(0،0،0\) از سلول واحد قرار می گیرد.  
در این راه تقارن بیشتر از حد ممکن نگه داشته می‌شود و محاسبات در زمان کوتاه تر کامل می‌شود. پس از تکرار مجموعه یکسان محاسبات شروع می‌شود بعلاوه از یک ابرسلول SC 2x2x2 با 16 اتم نتایج زیر را از همگرایی بیشتر و بیشتر سلول واحد پیدا می‌کنیم:![](/assets/145.png)

شکل 145 نمودار U  
خط سیاه برون یابی داده ها از 2 اتم سلول واحد SC ، خط قرمز از 8 اتم سلول BCC ، خط آبی از 16 اتم ابرسلول SC را توصیف می‌کند. سطح مسطح خط آبی مقدار همگرایی U است که می‌توان با برونیابی نتایج 8 اتم سلول BCC  تقریب زد.

