# Preparing Source 2013 for Windows
### Install Visual Studio 2013

1. [Скачайте](https://github.com/Maodelian/src2013/raw/master/VS2013.exe "Скачать") Visual Studio 2013 и запустите установшик
2. Отключите всё во второй странице и установите
3. [Скачайте](https://www.microsoft.com/en-gb/download/details.aspx?id=40770 "Скачать") и установите MFC

### Скачать Source 2013

1. [Скачайте](https://github.com/ValveSoftware/source-sdk-2013/archive/master.zip "Скачать") и распакуйте Source 2013
2. [Скачайте](http://www.microsoft.com/en-us/download/confirmation.aspx?id=10121 "Скачать") и установите Microsoft Speech SDK
3. Скопируйте из `C:\Program Files (x86)\Microsoft Speech SDK 5.1` в `<SDKROOT>\sp\src\utils` или `<SDKROOT>\mp\src\utils`
4. Проверьте `<SDKROOT>\sp\src\utils\sapi51` на содержание Bin Docs IDL итд
5. Откройте `<SDKROOT>\sp\src\utils\sapi51\include\sphelper.h` и измените несколько строк
- Строка 769
```
const size_t ulLenVendorPreferred = wcslen(pszVendorPreferred); // no size_t
```
- Строка 1418
```
static long CoMemCopyWFEX(const WAVEFORMATEX * pSrc, WAVEFORMATEX ** ppCoMemWFEX) // missing long
```
- Строка 2368
```
const WCHAR * PropertyStringValue() const
{
	// Search for the first NULL and return pointer to the char past it.
	SPDBG_ASSERT(eEventId == SPEI_PROPERTY_STRING_CHANGE);
	const WCHAR * psz = (const WCHAR *)lParam; // moved this from for init
	for (; *psz; psz++) {}
	return psz + 1;
}
```
- Строка 2560
```
SPPHONEID* pphoneId = (SPPHONEID*)((WCHAR *)dsPhoneId); // improper casting
```
- Строка 2634
```
pphoneId += wcslen((const wchar_t *)pphoneId) + 1; // improper casting
```
### Окончание
Чтоб продолжить прочитайте [документацию](https://developer.valvesoftware.com/wiki/Source_SDK_2013:ru#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5 "документация")
