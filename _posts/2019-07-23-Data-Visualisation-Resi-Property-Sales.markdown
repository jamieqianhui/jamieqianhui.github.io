---
layout: post
title:  "Data Visualisation in Tableau"
date:   2019-07-23 09:47:36 +0800
categories: Residential PropertySales
---
Are you looking to buy a private residential property in Singapore and wish to get a sensing of the market performance? Retrieving public datasets available on URA API reference site, I built a dashboard to analyse the **demand and supply for Singapore's Private Residential Property Sales in 1H2019**. Specifically, I dissected the dataset to identify the following trends: 1) Top 10 Sales Volume and Highest Median Price PSF by Developer and Project, 2) Sales Price PSF by Market Segment across period, 3) Take up rate (Launched units VS Sold Units) and 4) Median Price PSF by geographical location and individual project. ![viz]({{ '/assets/VIZ.PNG' | relative_url }}) 

<br>
<iframe seamless frameborder="0" src="https://public.tableau.com/views/SGPrivateResidentialPropertySales1H2019DemandSupply/SingaporePrivateResidentialPropertySales1H2019DemandvsSupply?:embed=y&:display_count=yes&:origin=viz_share_link" width = '1200' height = '1200' scrolling='yes' ></iframe>    

<br>
**Analysis:**
+ The average take up rate for median price PSF (>$2,500 psf) are generally lower, ranging below 40%. Cautious buyer sentiments who do not have strong conviction on the property's value appreciation potential could be one of the contributing factors. 
+ Private Residential Projects located in the Core Central Region (CCR) and Rest of Central Region (RCR) command higher median price PSF, ranging from $2,500 psf to $6,000 psf 
+ Projects located in district 9 and 10 generally fetch higher premium prices. This is largely due to the property's prime location and the product positioning of the residential project as a luxury class development. 
<br>

[Click here to visit my Tableau Public Viz Portfolio][tableau] 

[tableau]: https://public.tableau.com/profile/jamie.lu2833#!/vizhome/SGPrivateResidentialPropertySales1H2019DemandSupply/SingaporePrivateResidentialPropertySales1H2019DemandvsSupply
[urllib]: https://docs.python.org/3/library/urllib.request.html
[BS]: https://www.crummy.com/software/BeautifulSoup/bs4/doc/

