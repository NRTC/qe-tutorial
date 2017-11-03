1

##  اجرای بند استراکچر

پس از ریلکس شدن ساختار فایل های ورودی scf ، nscf ، bands، ban و plotbands را مانند زیر آماده می‌کنیم و نیاز است مراحل زیر طی شود، اما پیش از آن به توضیح ساختار نواری خواهیم پرداخت.

1. ./pw.x &lt;scf.in&gt; scf.out

2. ./pw.x &lt;ban.in&gt; ban.out

3. ./bands.x &lt;bands.in&gt; bands.out

4. ./plotband.x &lt;plotbands.in&gt; plotbands.out

که scf.in یک فایل ورودی برای محاسبات SCF است bands.in .یک فایل ورودی برای جمع آوری باند ها است k-point-path .این فایل حاوی لیستی ازk-point در جهت تقارن منطقه بریلوئن است.

فایلplotband.in یک فایل ورودی برای قرار دادن داده های band structure به فرمتplottable است.

