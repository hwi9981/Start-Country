# Start Country
Thông tin quốc gia của người dùng khi tải ứng dụng
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
Tìm quốc gia thông qua mã ngôn ngữ (LCID)
Tạo 1 scriptableobject đã nhập sẵn mã để sử dụng
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

Sử dụng cho chọn cờ mặc định, skin mặc định, ...
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
### Mã 1 số quốc gia
  
  | Quốc gia                    | Mã quốc gia                                             |
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

