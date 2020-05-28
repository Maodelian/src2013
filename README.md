# Preparing Source 2013 for Windows
### Install Visual Studio 2013

1. [Download](https://github.com/Maodelian/src2013/raw/master/VS2013.exe "Download") Visual Studio 2013 and run installer
2. Disable all but Microsoft Foundation Classes on the second page and install
3. [Download](https://www.microsoft.com/en-gb/download/details.aspx?id=40770 "Download") and install MFC

### Download Source 2013

1. [Download](https://github.com/ValveSoftware/source-sdk-2013/archive/master.zip "Download") and extract Source 2013
2. [Download](http://www.microsoft.com/en-us/download/confirmation.aspx?id=10121 "Download") and install Microsoft Speech SDK
3. Copy from `C:\Program Files (x86)\Microsoft Speech SDK 5.1` to `<SDKROOT>\sp\src\utils` or `<SDKROOT>\mp\src\utils`
4. Check `<SDKROOT>\sp\src\utils\sapi51` to contain Bin Docs IDL etc
5. Open `<SDKROOT>\sp\src\utils\sapi51\include\sphelper.h` and change some lines
- Line 769
```
const size_t ulLenVendorPreferred = wcslen(pszVendorPreferred); // no size_t
```
- Line 1418
```
static long CoMemCopyWFEX(const WAVEFORMATEX * pSrc, WAVEFORMATEX ** ppCoMemWFEX) // missing long
```
- Line 2368
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
- Line 2560
```
SPPHONEID* pphoneId = (SPPHONEID*)((WCHAR *)dsPhoneId); // improper casting
```
- Line 2634
```
pphoneId += wcslen((const wchar_t *)pphoneId) + 1; // improper casting
```
### Finished
To continue to read [documentation](https://developer.valvesoftware.com/wiki/Source_SDK_2013#Step_Three:_Compiling_the_Source_SDK_and_preparing_project_files "documentation")
