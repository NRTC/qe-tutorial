
محاسبه چگالی حالت الکترونی مواد مغناطیسی: 

برای اجرای چگالی حالت مواد مغناطیسی لازم است مانند حالت مواد مغناطیسی مراحل زیر با یک سری از ویرایشات انجام شود.
DOS
5. pw.x <scf.in> scf.out
6. pw.x <nscf.in> nscf.out
7. dos.x <dos.in> dos.out
8. projwfc.x <pdos.in> pdos.out

توجه داشته باشید برای انجام مراحل فوق کافیست در nscf ، occuoations را در حالت tetrahedra قرار دهید 

شکل 125 ورودی nscf برای DOS
در نتیجه نمودار DOS در حالت کلی به صورت شکل 126 و برای حالت اسپین up و down به صورت مجزا به صورت شکل 127 حاصل می‌شود :


شکل 126 نمودار DOS

شکل 127 نمودار DOS

اگر می خواهید چگالی حالت الکترونی و ساختار نواری را بصورت پیوسته انجام دهیم لازم است مراحل زیر طی شود:

10. pw.x <scf.in> scf.out
11. pw.x <nscf.in> nscf.out
12. pw.x <ban.in> ban.out
13. bands.x <bands.in> bands.out
14. plotband.x <plotband.in> plotband.out
15. dos.x <dos.in> dos.out
16. projwfc.x <pdos.in> pdos.out







همچنین فایل های ورودی و خروجی برنامه DOS و Bands را به صورت پیوسته می‌توانید در شکل 128 ببینید



شکل 128 ورودی و خروجی DOS و bands
