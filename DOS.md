
1.9-    DOS(چگالی حالتهای الکترونی)
برای محاسبه چگالی حالتها  لازم است مراحل nscf, scf  و dos انجام می گیرند که به ترتیب در قسمت زیر مشاهده می‌کنید.
:DOS
1. pw.x <scf.in> scf.out
2. pw.x <nscf.in> nscf.out
3. dos.x <dos.in> dos.out
4. projwfc.x <pdos.in> pdos.out

در اینجا نیز مانند بنداستراکچر یا همان ساختار نواری باید از برنامه ورودی (شکل 39 )scf  بگیریم. همانطور که گفته شد ران برنامه ها را در محیط ترمینال به صورت	pw.x <scf.in> scf.out انجام می دهیم. پس از scf  باید از فایل ورودی nscf بگیریم فقط توجه کنید که در فایل ورودی nscf   شکل 56
علاوه بر اصلاح خط 1 و 6 و 7 به تناسب نوع محاسبه و محل فایل شبه پتانسیل و خروجی، خط 20 و 21 اضافه می‌شود که در فایل scf  نیست و خط 21 به معنی عدم استفاده از تقارن در محاسبات است. همچنین میدانیم در scf  باید انرژی کات و کاپوینت بهینه باشند فرض کنید انرژی کات بهینه scf 30 الکترون ولت می‌باشد. برای محاسبه nscf  در dos  باید این انرژی و کاپوینت بیشتر باشد مانند شکل 56 که انرژی 70 و به تناسب آن خط بعدی  ده برابر آن است، زیرا غیر خودسازگار است و با انجام یک حلقه محاسبات تمام می‌شود 


شکل 55  قسمتی از فایل ورودی nscf


شکل 56  ادامه فایل ورودی nscf 

سپس نوبت مرحله ی سوم یعنی DOS است. همانطور که در شکل 57 می بینید در اینجا علاوه بر مسیر فایل خروجی کمترین و بیشترین میزان انرژی مشخص شده است و در  خروجی برنامه  علاوه بر dos.out  یک فایل dos  شکل 58 می دهد که مورد استفاده است.



شکل 57  فایل ورودی  Dos گرافن  


شکل 58 قسمتی از فایل dos که در خروجی ایجاد می‌شود.
در شکل 58 در ستون اول میزان انرژی الکترون ها (بر حسب الکترون ولت ) و در ستون دوم dos  یا چگالی حالتهای الکترونی را مشاهده می‌کنید که اگر آن را در نرم افزاری مانند اریجین رسم کنیم شکل 59وشکل 60 را مشاهده خواهید کرد. اگر دقت کرده باشید در این پروسه از گرافن استفاده کرده ایم و چون می خواهیم DOS بگیریم در فایل ورودی nscf، در قسمت system، occupation  را tetrahedral  می‌کنیم .

    occupations = 'tetrahedra' ,
    

شکل 59 نمودار dos  در اریجین زمانی که accupation  تتراهدرا نباشد.

شکل 60 نمودار dos  با  accuapation=tetrahedra 
برای مقایسه بهتر می‌توان dos و bandestructur  را در یک نمودار رسم کرد شکل 61.

شکل 61 نمودار dod و band گرافن
در انتها مرحله چهارم یا pdos است که چگالی اربیتال های الکترونی را نشان می دهد. در شکل 62 نمونه ای از فایل ورودی pdos را مشاهده می‌کنید.


شکل 62 فایل ورودی pdos گرافن

    در قسمت خروجی چون گرافن، ساخته شده از دو کربن است و عدد اتمی یا الکترون های کربن 6 است به ترتیب با اربیتال های 1s2 ،2s2 و 2p2 پر می‌شود بنابراین چگالی اربیتال های لایه ظرفیت شامل s وp  با دو اتم کربن نشان داده می‌شوند مانند شکل زیر:


شکل 63 فایل های ورودی و خروجی pdos  گرافن
پس از باز کردن خروجی اربیتال s  کربن شکل 64 را مشاهده می‌کنید که ستون اول انرژی و ستون دوم و ستون سوم چگالی اربیتال است. در اینجا چون جهت گیری فضایی اربیتال s  به شکل کروی است سه ستون است، اما اگر شکل 65 اربیتالp  را بنگرید به دلیل جهت گیری فضایی در راستای x،y  و z ستون های دیگری نیز وجود دارد.

شکل 64 بخشی از خروجی اربیتال s  فایل pdos


شکل 65 بخشی ازخروجی اربیتال p  فایل pdos

به ترتیب نمودار فایل خروجی اربیتال s  در اریجین به صورت شکل 66 و نمودارهای اربیتال p  در راستای x,y به  و در راستایz  به شکل 68 است. همانطور که می بینید در راستای x,y تقریبا مشابه همند چون در یک صفحه  می‌باشند.


شکل 66 نمودار اربیتال s  گرافن حاصل ازخروجی pdos


شکل 67 نمودار اربیتال  py وpx گرافن حاصل ازخروجی pdos















شکل 68 نمودار اربیتال   pz گرافن حاصل ازخروجی pdos

در انتها چگالی اربیتال های نیتروژن را در شکل 69 می‌توانید با گرافن مقایسه کنید و گاف رسانش را 
در محدوده 



شکل 69 نمودار اربیتال   p وs  نیتروژن حاصل ازخروجی pdos  