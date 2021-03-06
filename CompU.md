## محاسبه U

میدانیم U به عنوان مشتق دوم انرژی با توجه به اعداد occupation در محل محاسبه شده است.  
یک جمله غیر تعاملی \(با توجه به iteration هیبریداسیون از اوربیتال\) کم شده است :

$$U=\frac{d^2 E^{GGA}}{d(n^I)^{2}}-\frac{d^2 E_0^{GGA}}{d (n^I)^{2}}$$

مشتقات دوم در این عبارات با یک پاسخ خطی نزدیک به پاسخهای مطالعه شده سیستم \( تغییر در محل occupation \) به یک اختلال در حالات محلی از یک " هابارد" اتم ظاهر می‌شود:

$$\Delta V=\alpha\sum_m|\varphi_m^I><\varphi_m^I|$$

اگر تعریف کنیم :

$$x_{IJ}^0=\frac{d n_0^I}{d \alpha_J}$$

$$x_{IJ}=\frac{d n^I}{d \alpha_J}$$

می‌توانیم U را به صورت زیر بنویسیم :

$$U=-\frac{d \alpha_I}{d n^I}+\frac{d \alpha_I}{d n_0^I}=(x_0^{-1}-x^{-1})_{II}$$

بنابراین هدف ما محاسبه پاسخ دو ماتریس X و X0 است . ما از طریق مراحل زیر پیش میرویم :  
1\) اجرای یک محاسبه SCF بدون اختلال  
2\) با شروع از پتانسیل ذخیره شده از محاسبه SCF یک سری از محاسبات را برای چند مقدار آلفا در اطراف 0 انجام می‌دهیم.  
3\) با مطالعه پاسخ \(خطی\)تمام occupation ها در محل ماتریس پاسخ را میسازیم.  
4\)آنها را انحراف داده و اختلافشان را بدست می آوریم. عناصر قطری پارامترهای U روی اتمهای مختلف خواهد بود.  
اختلال به کار برده شده باید جدا شود : ما نمی خواهیم که اختلال دوره ای اتم های مکرر با یکدیگر تداخل داشته باشد. بنابراین معمولا از ابرسلولها با افزایش اندازه استفاده می‌کنیم \(تا زمانیکه U به همگرایی برسد \). اطلاعات به دست آمده از سلول های کوچکتر نیز می‌تواند به سلولهای بزرگتر تعمیم داده شود در این فرضیه  بیشترین لایه ها از همسایه ها به طور قابل توجهی در پاسخ شرکت داده نمی شود.  
برای درک بهتر این مفاهیم به بررسی دو مثال  می‌پردازیم.

