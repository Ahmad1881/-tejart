# -tejart
Baraye ahmad asghari xeyremasjedi 
معرفی

در مقاله قبلی خود ، من به شما نشان دادم که چگونه با استفاده از اشیاء متاتریدر 5، یک Chart Trade ایجاد کنید و بنابراین پلتفرم را به یک سیستم RAD تبدیل کنید. این سیستم بسیار خوب کار می کند، و مطمئناً بسیاری از خوانندگان ممکن است به ایجاد یک کتابخانه فکر کرده باشند، که امکان داشتن عملکرد گسترده در سیستم پیشنهادی را فراهم می کند. بر این اساس، می توان یک مشاور متخصص بصری تر با رابط کاربری زیباتر و آسان تر ایجاد کرد.

این ایده به قدری خوب است که من را بر آن داشت تا گام به گام نحوه شروع افزودن قابلیت را به شما نشان دهم. در اینجا من قصد دارم دو ویژگی جدید و اصلی را پیاده سازی کنم (این اطلاعات به عنوان پایه ای برای پیاده سازی سایر ویژگی ها به روشی که نیاز داریم و می خواهیم). تنها محدودیت، خلاقیت ماست، زیرا خود عناصر می توانند به طرق مختلف مورد استفاده قرار گیرند.


برنامه ریزی

تغییرات IDE ما مانند تصاویر زیر خواهد بود:

          

همانطور که می بینید، تغییرات جزئی در خود طراحی وجود دارد. دو منطقه جدید اضافه شده است: یکی نام دارایی را دریافت می کند و دیگری ارزش انباشته روز را دریافت می کند. خوب، اینها چیزهایی هستند که می توانیم بدون آنها زندگی کنیم و تاثیری بر تصمیمات ما نخواهد داشت. اما به هر حال می توانند جالب باشند. من ساده ترین و صحیح ترین راه را برای افزودن قابلیت به IDE نشان خواهم داد. بنابراین، لیست اشیاء را در رابط جدید باز کنید. به صورت زیر ظاهر می شود:


دو شیء محاصره شده رویدادهای مرتبط با آنها را ندارند، به این معنی که آنها در IDE عمل نمی کنند. همه اشیاء دیگر قبلاً به درستی با رویدادهای خاصی مرتبط شده اند و متاتریدر 5 می تواند این رویدادها را در صورت وقوع در EA مجبور کند به درستی اجرا شوند. یعنی ما می‌توانیم رابط IDE را به دلخواه تغییر دهیم، اما اگر این قابلیت هنوز پیاده‌سازی نشده باشد، متاتریدر 5 کاری جز نمایش شی در نمودار انجام نمی‌دهد. برای دریافت نام دارایی مورد معامله به شی EDIT 00 نیاز داریم و این نام باید در مرکز شی ظاهر شود. شی EDIT 01 مقدار انباشته شده را برای یک دوره معین دریافت می کند. ما از دوره روزانه استفاده خواهیم کرد تا بدانیم در طول روز در سود هستیم یا زیان. در صورت منفی بودن مقدار به صورت یک رنگ و در صورت مثبت بودن از رنگ دیگری استفاده می شود.

بدیهی است که کاربر نمی تواند هر دو مقدار را تغییر دهد، بنابراین می توانید مشخصات آنها را فقط خواندنی بگذارید، همانطور که در شکل زیر نشان داده شده است.



با این حال، به خاطر داشته باشید که نمی توان نحوه ارائه اطلاعات را مشخص کرد، یعنی نمی توانیم متن را طوری تراز کنیم که در مرکز شی ظاهر شود. در صورت تمایل، می توان این کار را با استفاده از کد انجام داد، زیرا یک ویژگی وجود دارد که متن را در مرکز تنظیم می کند. برای جزئیات بیشتر به " ویژگی های شی " مراجعه کنید. لطفاً به ENUM_ALIGN_MODE در جدول توجه داشته باشید - شامل اشیایی است که می توانید از متن توجیه شده روی آنها استفاده کنید .

بنابراین، هر اصلاحی که می‌خواهیم اعمال کنیم، اولین کاری که باید انجام دهیم این است که یک طرح آماده کنیم: تعریف ویژگی‌های جدید، فرم ارائه آنها و روش‌هایی که کاربر با آنها تعامل خواهد داشت. این امکان انتخاب شی مناسب و پیکربندی آن را تا حد امکان با استفاده از رابط شخصی متاتریدر 5 فراهم می کند. در نتیجه یک IDE آماده خواهیم داشت و فقط باید آن را از طریق کد MQL5 تنظیم کنیم تا IDE در نهایت 100% کارایی داشته باشد. بنابراین، اجازه دهید به اصلاحات ادامه دهیم.


اصلاحات

برای جلوگیری از تبدیل شدن کد به یک فرانکشتاین واقعی، باید تا حد امکان خودمان را سازماندهی کنیم تا بررسی کنیم که کدام ویژگی از قبل وجود دارد و کدام یک واقعاً نیاز به پیاده سازی دارند. در بسیاری از موارد، ایجاد تغییرات جزئی در کد موجود، دریافت کد جدید و آزمایش آن کافی است. این کد جدید در کدی که می‌خواهیم پیاده‌سازی کنیم دوباره استفاده می‌شود و تنها چیزی که برای آزمایش باقی می‌ماند توابع کنترل کوچکی است که برای ایجاد عملکرد کاملاً جدید اضافه خواهیم کرد. برنامه نویسان خوب همیشه این کار را انجام می دهند: آنها سعی می کنند از طریق اضافه کردن نقاط کنترل به کد موجود، دوباره از کد موجود استفاده کنند.


اصلاح 1. افزودن نام دارایی

برای اجرای این قسمت نیازی به تغییرات اساسی نداریم بلکه این تغییرات باید در مکان های مناسب پیاده سازی شوند. ابتدا، بیایید یک مقدار جدید به شمارش اضافه کنیم، کد منبع در زیر نشان داده شده است:

تعداد eObjectsIDE {eRESULT، eBTN_BUY، eBTN_SELL، eCHECK_DAYTRADE، eBTN_CANCEL، eEDIT_LEVERAGE، eEDIT_TAKE، eEDIT_STOP}؛ 

در زیر کد جدید آمده است؛ قسمت برجسته چیزی است که اضافه شده است. لطفاً توجه داشته باشید که من مقدار جدید را به ابتدا یا انتهای شمارش اضافه نمی کنم. این کار برای جلوگیری از به هم ریختن سایر بخش های کد که از قبل وجود دارد و کار می کند انجام می شود.

تعداد eObjectsIDE {eRESULT، eLABEL_SYMBOL ، eBTN_BUY، eBTN_SELL، eCHECK_DAYTRADE، eBTN_CANCEL، eEDIT_LEVERAGE، eEDIT_TAKE، eEDIT_STOP}؛ 

اگر مقدار جدید را در ابتدا یا در پایان شمارش اضافه کنید، باید تمام مکان‌هایی را که از این محدودیت‌ها استفاده شده است، پیدا کرده و تغییر دهید. در بسیاری از موارد می توان به دلیل فراموشی مواردی را حذف کرد که به خطاهایی منجر می شود که یافتن آنها دشوار خواهد بود. ممکن است فکر کنید که خطاها به دلیل اضافات جدید هستند، در حالی که در واقع به دلیل فراموشی هستند. بنابراین، ما تغییرات را در جایی بین مقادیر شدید اضافه می کنیم.

بلافاصله پس از آن باید یک پیام به سیستم اضافه کنیم، در غیر این صورت ممکن است با خطای RunTime مواجه شویم. بنابراین، خط زیر را به کد منبع خود اضافه کنید.

string const static C_Chart_IDE::szMsgIDE[] = {                                                  "MSG_RESULT" ,                                                  "MSG_NAME_SYMBOL" , "MSG_BUY_MARKET" ,                                                  "MSG_SELL_MARKET" ,                                                  "MSG_DAY_TRADE" ,                                                  "MSG_CLOSE_MS" ,                                                  "MSG_CLOSE_POGUE ,                                                  " MSG_CLOSE_MS                                                  "                                                                                                 "MSG_STOP_VALUE"                                               }; 


همانطور که می بینید، برای حفظ سفارش آن را در همان مکان اضافه کرده ایم. اما در لحظه ای که ثابت را می توان در هر نقطه اضافه کرد، هیچ تفاوتی نخواهد داشت زیرا فقط برای بررسی اینکه کدام شی پیام را دریافت می کند استفاده می شود. برای اهداف ساختاری، آن را به عنوان پیام دوم اضافه کردیم.

حالا بیایید به متاتریدر 5 برگردیم و تغییرات را مطابق شکل زیر انجام دهیم:

          

اکنون، متاتریدر 5 از قبل شیء موجود در IDE ما را به عنوان یک شی برای دریافت پیام تشخیص می دهد، و تنها ایجاد یک رویه برای ارسال پیام باقی می ماند. متن به پیام باید فقط یک بار اضافه شود و به محض اینکه MetaTrader 5 IDE ما را در نمودار قرار داد می توان آن را ارسال کرد. این کار را می‌توان با افزودن کد لازم به انتهای تابع Create کلاس شی ما انجام داد. اما دوباره، برای اینکه کد به فرانکنشتاین پر از اصلاحات تبدیل نشود ، کد جدید را در تابع DispatchMessage اضافه می کنیم. تابع اصلی به شکل زیر است:

void DispatchMessage ( int iMsg، string szArg، double dValue = 0.0 ) {         اگر (m_CountObject < eEDIT_STOP) بازگشت ;         سوئیچ (imsg)         {                 مورد CHARTEVENT_CHART_CHANGE :                          اگر (szArg == szMsgIDE[eRESULT])                         {                                 ObjectSetInteger (Terminal.Get_ID()، m_ArrObject[eRESULT].szName، OBJPROP_BGCOLOR ، (dValue < 0 ? clrLightCoral : clrLightGreen ));                                 ObjectSetString (Terminal.Get_ID()، m_ArrObject[eRESULT].szName, OBJPROP_TEXT , DoubleToString (dValue, 2 ));                         }                         شکستن ;                 مورد CHARTEVENT_OBJECT_CLICK : // ... بقیه کد ...         } } 


در زیر کد پس از تغییرات مربوطه آمده است:

void DispatchMessage ( int iMsg، string szArg، double dValue = 0.0 ) {         اگر (m_CountObject < eEDIT_STOP) بازگشت ;         سوئیچ (imsg)         {                 مورد CHARTEVENT_CHART_CHANGE :                          اگر (szArg == szMsgIDE[eRESULT])                         {                                 ObjectSetInteger (Terminal.Get_ID()، m_ArrObject[eRESULT].szName، OBJPROP_BGCOLOR ، (dValue < 0 ? clrLightCoral : clrLightGreen ));                                 ObjectSetString (Terminal.Get_ID()، m_ArrObject[eRESULT].szName, OBJPROP_TEXT , DoubleToString (dValue, 2 ));                         } else if (szArg == szMsgIDE[eLABEL_SYMBOL])                         {                                 ObjectSetString (Terminal.Get_ID(), m_ArrObject[eLABEL_SYMBOL].szName, OBJPROP_TEXT , Terminal.GetSymbol();                                 ObjectSetInteger(Terminal.Get_ID(), m_ArrObject[eLABEL_SYMBOL].szName, OBJPROP_ALIGN , ALIGN_CENTER );                         }                         شکستن ;                 مورد CHARTEVENT_OBJECT_CLICK : // ... بقیه کد         } } 
 پیام را ارسال می کنیم، انتخاب کنیم. بهترین مکان در واقع در انتهای تابع Create کلاس شی ما است، بنابراین کد نهایی به شکل زیر خواهد بود:

bool Create ( int nSub) {         m_CountObject = 0 ;         if ((m_fp = FileOpen ( "Chart Trade\\IDE.tpl" , FILE_BIN | FILE_READ )) == INVALID_HANDLE ) return false ;         FileReadInteger (m_fp، SHORT_VALUE )؛                                          برای (m_CountObject = eRESULT; m_CountObject <= eEDIT_STOP; m_CountObject++) m_ArrObject[m_CountObject].szName = "" ;         m_SubWindow = nSub;         m_szLine = "" ;         در حالی که (m_szLine != "</chart>" )         {                 اگر (!FileReadLine() ) false ;                 اگر (m_szLine == "<object>" )                 {                         اگر (!FileReadLine() ) false ;                         اگر (m_szLine == "نوع" )                         {                                 if (m_szValue == "102" ) if (!LoopCreating( OBJ_LABEL ) ) false ;                                 if (m_szValue == "103" ) if (!LoopCreating( OBJ_BUTTON ) ) false ;                                 if (m_szValue == "106" ) if (!LoopCreating( OBJ_BITMAP_LABEL ) ) false ;                                 if (m_szValue == "107" ) if (!LoopCreating( OBJ_EDIT )) return false ;                                 if (m_szValue == "110" ) if (!LoopCreating( OBJ_RECTANGLE_LABEL ) ) false ;                         }                 }         }         FileClose (m_fp)؛         DispatchMessage( CHARTEVENT_CHART_CHANGE ، szMsgIDE[eLABEL_SYMBOL]);         بازگشت درست _ } 

اضافه شده در واقع با رنگ سبز مشخص شده است. توجه داشته باشید که بدون ایجاد تقریباً هیچ تغییری، ما در حال حاضر یک جریان پیام 100٪ پیاده سازی شده داریم و می توانیم به پیام بعدی که باید پیاده سازی شود، برویم.


اصلاح 2. افزودن مقدار انباشته شده برای روز (نقطه پوشش)

باز هم از همان منطقی پیروی می کنیم که هنگام اضافه کردن نام دارایی انجام دادیم و بنابراین کد جدید به شکل زیر خواهد بود:

تعداد eObjectsIDE {eRESULT، eLABEL_SYMBOL، eROOF_DIARY ، eBTN_BUY، eBTN_SELL، eCHECK_DAYTRADE، eBTN_CANCEL، eEDIT_LEVERAGE، eEDIT_TAKE، eEDIT_STOP}. // ... بقیه کد string const static C_Chart_IDE::szMsgIDE[] = {                                                  "MSG_RESULT" ,                                                  "MSG_NAME_SYMBOL" ,                                                  "MSG_ROOF_DIARY" , "MSG_BUY_MARKET" ,                                                  "MSG_SELL_MARKET" ,                                                  " MSG_SELL_MARKET" ,                                                  "MSG_SEG, "DEG_SEG," MSG_SEG ,                                                  "LOG_SEG" ،                                                  MSG_SYMBOL                                                                                                 "MSG_TAKE_VALUE" ،                                                  "MSG_STOP_VALUE"                                               }; 

پس از آن، اجازه دهید IDE را با یک پیام جدید تغییر دهیم:

          

IDE جدید ما آماده است. اکنون کدی را پیاده سازی می کنیم که پیامی حاوی مقدار انباشته شده برای روز ایجاد می کند. ابتدا باید تصمیم بگیریم که این ویژگی در کدام کلاس پیاده سازی شود. بسیاری از افراد احتمالاً این تابع را در اینجا، در کلاس C_Chart_IDE ایجاد می کنند، اما به دلایل سازمانی بهتر است آن را با توابعی که با سفارشات کار می کنند قرار دهیم. بنابراین کد در کلاس C_OrderView پیاده سازی می شود. کد آن 

کد آن در زیر نشان داده شده است:

Double UpdateRoof ( باطل ) {            بلیط          ulong ; int      max;         string   szSymbol = Terminal.GetSymbol();         دو برابر   انباشته = 0 ;                                          HistorySelect (macroGetDate( TimeLocal ())، TimeLocal ());         حداکثر = HistoryDealsTotal ();         برای ( int c0 = 0 ؛ c0 < max; c0++) if ((ticket = HistoryDealGetTicket (c0)) > 0 )                  if ( HistoryDealGetString (بلیت، DEAL_SYMBOL ) == szSymbol)                         انباشته += HistoryDealGetDouble (بلیت، DEAL_PROFIT )؛                                                          بازگشت انباشته; } 

اکنون که کد پیاده سازی شده است، باید پیام را به سیستم اضافه کنیم. برای آسان‌تر کردن زندگی اپراتور، من قبلاً کدی را برای گزارش نتایج نهایی اضافه کرده‌ام. اینم کدش:

void DispatchMessage ( int iMsg، string szArg، double dValue = 0.0 ) {         استاتیک دوبل AccumulatedRoof = 0.0 ;         bool     b0;         دو برابر   d0; اگر (m_CountObject < eEDIT_STOP) بازگشت ;         سوئیچ (imsg)                  {                 مورد CHARTEVENT_CHART_CHANGE :                          اگر ((b0 = (szArg == szMsgIDE[eRESULT])) || (szArg == szMsgIDE[eROOF_DIARY]) )                         {                                 اگر (b0)                                 {                                         ObjectSetInteger (Terminal.Get_ID()، m_ArrObject[eRESULT].szName، OBJPROP_BGCOLOR ، (dValue < 0 ? clrLightCoral : clrLightGreen ));                                         ObjectSetString (Terminal.Get_ID()، m_ArrObject[eRESULT].szName, OBJPROP_TEXT , DoubleToString (dValue, 2 ));                                 } دیگر                                 {                                         سقف انباشته = dValue;                                         dValue = 0 ;                                 }                                 d0 = سقف انباشته + dValue.                                 ObjectSetString (Terminal.Get_ID()، m_ArrObject[eROOF_DIARY].szName، OBJPROP_TEXT ، DoubleToString ( MathAbs (d0)، 2 ));                                 ObjectSetInteger (Terminal.Get_ID()، m_ArrObject[eROOF_DIARY].szName, OBJPROP_BGCOLOR , (d0 >= 0 ? clrForestGreen : clrFireBrick ));                         } else    if (szArg == szMsgIDE[eLABEL_SYMBOL])                         {                                 ObjectSetString (Terminal.Get_ID()، m_ArrObject[eLABEL_SYMBOL].szName، OBJPROP_TEXT ، Terminal.GetSymbol());                                 ObjectSetInteger (Terminal.Get_ID()، m_ArrObject[eLABEL_SYMBOL].szName، OBJPROP_ALIGN ، ALIGN_CENTER );                         }                         شکستن ;                 مورد CHARTEVENT_OBJECT_CLICK : // .... بقیه کد ....         } } 

قسمت های هایلایت شده سیستم را همانطور که در بالا توضیح دادیم پشتیبانی می کنند. اگر پیاده سازی به این صورت اجرا نمی شد، باید دو پیام به سیستم ارسال می کردیم تا اطلاعات به درستی به روز شود. اما با استفاده از روش پیاده‌سازی کد، می‌توانیم نتیجه هر دو موقعیت باز و نتیجه روز را با یک پیام ردیابی کنیم.

تغییر دیگری در EA مربوط به عملکرد OnTrade است. به نظر می رسد این است:

void OnTrade () {         SubWin.DispatchMessage( CHARTEVENT_CHART_CHANGE ، C_Chart_IDE::szMsgIDE[C_Chart_IDE::eROOF_DIARY]، NanoEA.UpdateRoof());         NanoEA.UpdatePosition(); } 

اگرچه این سیستم کار می کند، اما باید مراقب زمان اجرای عملکرد OnTrade باشید که همراه با OnTick ممکن است عملکرد EA را کاهش دهد. در مورد کد موجود در OnTick ، خیلی خوب نیست و بهینه سازی بسیار مهم است. اما با OnTrade آسان تر است ، در حالی که تابع در واقع زمانی فراخوانی می شود که تغییری در موقعیت وجود داشته باشد. با دانستن این موضوع، ما دو گزینه داریم. اولین مورد تغییر موقعیت UpdateRoof برای محدود کردن زمان اجرای آن است. جایگزین دیگر این است که خود تابع OnTrade را تغییر دهید. به دلایل عملی، سقف آپدیت را اصلاح خواهیم کردعملکرد و بنابراین زمانی که یک موقعیت باز داشته باشیم حداقل زمان اجرا را کمی بهبود خواهیم داد. عملکرد جدید به شرح زیر است:

Double UpdateRoof ( باطل ) {                    بلیط          ulong ; string   szSymbol = Terminal.GetSymbol();         int              max;         static int       memMax = 0 ;         استاتیک دو برابر    انباشته = 0 ;                          HistorySelect (macroGetDate( TimeLocal ())، TimeLocal ());         حداکثر = HistoryDealsTotal ();         اگر (memMax == max) بازگشت Accumulated; else
