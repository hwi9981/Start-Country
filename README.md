# Start Country
The language the user's operating system is running in
### The simplest and easiest way
use Application.systemLanguage. It's data type is an enum in unity library
```csharp
namespace UnityEngine
{
    public enum SystemLanguage
    {
        Afrikaans = 0,
        Arabic = 1,
        Basque = 2,
        Belarusian = 3,
        Bulgarian = 4,
        Catalan = 5,
        Chinese = 6,
        Czech = 7,
        Danish = 8,
        Dutch = 9,
        English = 10,
        Estonian = 11,
        Faroese = 12,
        Finnish = 13,
        French = 14,
        German = 15,
        Greek = 16,
        Hebrew = 17,
        Hugarian = 18,
        Hungarian = 18,
        Icelandic = 19,
        Indonesian = 20,
        Italian = 21,
        Japanese = 22,
        Korean = 23,
        Latvian = 24,
        Lithuanian = 25,
        Norwegian = 26,
        Polish = 27,
        Portuguese = 28,
        Romanian = 29,
        Russian = 30,
        SerboCroatian = 31,
        Slovak = 32,
        Slovenian = 33,
        Spanish = 34,
        Swedish = 35,
        Thai = 36,
        Turkish = 37,
        Ukrainian = 38,
        Vietnamese = 39,
        ChineseSimplified = 40,
        ChineseTraditional = 41,
        Hindi = 42,
        Unknown = 43,
    }
}
```
# Other way
### Demo Code
```csharp
using System.Globalization;
using UnityEngine;

public class CountryInfo : MonoBehaviour
{
    void Start()
    {
        RegionInfo region = new RegionInfo(CultureInfo.CurrentCulture.Name);
        string countryName = region.DisplayName;

        Debug.Log("Player is downloading from: " + countryName);
    }
}
```
### Demo Code
Find country by language code (LCID)
Create a scriptableobject with a pre-filled code to use
```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using System.Linq;
[CreateAssetMenu]
public class CountryData : ScriptableObject
{
    public Country[] allCountries;
    [System.Serializable]
    public class Country
    {
        public string Name;
        public int LCID; // area code
        public Sprite Flag;
    }
    public Country GetCountry(int LCID)
    {
        var result = allCountries.FirstOrDefault(x => x.LCID == LCID);
        return result != null ? result : allCountries[0];
    }
}
```
Used for selecting default flag, default skin, ...
```csharp
using System.Globalization;
using UnityEngine;

public class StartCountry : MonoBehaviour
{
    [SerializeField] CountryData _data;  
    private void Start()
    {
        var countryData = _data.GetCountry(CultureInfo.CurrentCulture.LCID);
    }
}
```
### Country code
  
  | Country                   | Country code                                             |
| ---------------------------------- | ---------------------------------------------------- |
United States	| 1033
United Kingdom	|	2057
Australia	|	3081
Canada	|	4105
France	|	1036
Germany	|	1031
Italy	|	1040
Spain	|	3082
Japan	|	1041
China	|	2052
South	Korea	| 1042
Vietnam	|	1066
Russia	|	1049
Brazil	|	1046
Mexico	|	2058
India	|	1081
Indonesia	|	1057
Netherlands	|	1043
Turkey	|	1055
Argentina	|	11274
Saudi Arabia	|	1025
Thailand	|	1054

