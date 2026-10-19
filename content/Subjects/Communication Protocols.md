# SPI

==Master== is the controller
==Slave== is the device

![[SPI-1779974804075.webp]]
<font color="#7030a0">SCK</font> is the clock
<font color="#00b050">SDO</font> Serial data out = <font color="#00b050">MOSI</font> Master out slave in
<font color="#92d050">SDI</font> Serial data in = <font color="#92d050">MISO</font> Master in slave out 
<font color="#00b0f0">CS</font> Chip select

> [!note]
> There is no stander in SPI so u may found alot of pins naming (:

![[SPI-1779976185494.webp]]
for 3 or more SPI in the same pins, u can use a decoder

---
# Ethernet

في توصيل الإيثرنت في جهازك

![[Pasted image 20260729221709.png]]

يوجد لدينا 3 طرق تواصل رئيسية
بداية انت تقوم بالتحويل إلى ال PHY layer من خلال ال PHY ثم ال soc أو ال MCU يقوم بالتحويل إلى MAC من خلال الجزء الداخلي الموجود داخله

الأن التواصل مع ال PHY الخارجية يكون من خلال واجهتين اساسيتيين
- ال MII أو مشتقاتها (الهدف من G تعريف ان النقل ل 1GB من البيانات و ال R لتقليل عدد خطوط التوصيل من 8 إلى 4) و هي البيانات الأساسية
- ال MDIO هنا تتحدث عملية التفاوض و التوصيل و تعريف كيف يتم تشغيل الليدات و غيرها و يمكن تشبيهها ب I2C

---
# RGMII

![[Pasted image 20260729222304.png]]

