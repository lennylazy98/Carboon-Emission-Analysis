#1 Which products contribute the most to carbon emissions?

SELECT product_name, sum(carbon_footprint_pcf) as the_most_to_carbon_emissions
FROM product_emissions
GROUP BY 1
ORDER BY 2 desc
LIMIT 10

| product_name                                                                                                                       | the_most_to_carbon_emissions | 
| ---------------------------------------------------------------------------------------------------------------------------------: | ---------------------------: | 
| Wind Turbine G128 5 Megawats                                                                                                       | 3718044                      | 
| Wind Turbine G132 5 Megawats                                                                                                       | 3276187                      | 
| Wind Turbine G114 2 Megawats                                                                                                       | 1532608                      | 
| Wind Turbine G90 2 Megawats                                                                                                        | 1251625                      | 
| TCDE                                                                                                                               | 198150                       | 
| Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.                                                                 | 191687                       | 
| Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall | 167000                       | 
| Electric Motor                                                                                                                     | 160655                       | 
| Audi A6                                                                                                                            | 111282                       | 
| Average of all GM vehicles produced and used in the 10 year life-cycle.                                                            | 100621                       | 


#2 What are the industry groups of these products?

SELECT  i.industry_group, sum(carbon_footprint_pcf), product_name
FROM product_emissions p
LEFT JOIN industry_groups as i ON i.id = p.industry_group_id
GROUP BY 1
ORDER BY 2 desc
LIMIT 10

| industry_group                                   | sum(carbon_footprint_pcf) | product_name                                                                                                                                                                                                                                                                                                                                                                            | 
| -----------------------------------------------: | ------------------------: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | 
| Electrical Equipment and Machinery               | 9801558                   | ACTI9 IID K 2P 40A 30MA AC-TYPE RESIDUAL CURRENT CIRCUIT BREAKER                                                                                                                                                                                                                                                                                                                        | 
| Automobiles & Components                         | 2582264                   | VW Polo V 1.6 TDI BlueMotion Technology                                                                                                                                                                                                                                                                                                                                                 | 
| Materials                                        | 577595                    | KURALON  fiber                                                                                                                                                                                                                                                                                                                                                                          | 
| Technology Hardware & Equipment                  | 363776                    | Multifunction Printers                                                                                                                                                                                                                                                                                                                                                                  | 
| Capital Goods                                    | 258712                    | Office Chair                                                                                                                                                                                                                                                                                                                                                                            | 
| "Food, Beverage & Tobacco"                       | 111131                    | Frosted Flakes(R) Cereal                                                                                                                                                                                                                                                                                                                                                                | 
| "Pharmaceuticals, Biotechnology & Life Sciences" | 72486                     | Alliance HPLC (High Peformance Liquid Chromatography)  The Alliance is an HPLC that is unique in that it has a single set of electronic boards that control the functions for both the solvent delivery system and the autosampler in the liquid chromatograph.                                                                                                                         | 
| Chemicals                                        | 62369                     | Mobile Batteries                                                                                                                                                                                                                                                                                                                                                                        | 
| Software & Services                              | 46544                     | USB software                                                                                                                                                                                                                                                                                                                                                                            | 
| Media                                            | 23017                     | "Bloomberg's standard-issue flat panel configuration (prior to 2010) was two 19\" panels mounted on a metal stand. In early 2010 Bloomberg engaged in the WRI Product Life Cycle Roadtest for this functional unit (cradle-to-grave). The functional unit has a lifespan of 5 years, so the emissions indicated [in this report] are the full emissions associated with that lifespan." | 

#3 What are the industries with the highest contribution to carbon emissions?


SELECT  i.industry_group, sum(carbon_footprint_pcf)
FROM product_emissions p
LEFT JOIN industry_groups as i ON i.id = p.industry_group_id
GROUP BY 1
ORDER BY 2 desc
LIMIT 10


| industry_group                                   | sum(carbon_footprint_pcf) | 
| -----------------------------------------------: | ------------------------: | 
| Electrical Equipment and Machinery               | 9801558                   | 
| Automobiles & Components                         | 2582264                   | 
| Materials                                        | 577595                    | 
| Technology Hardware & Equipment                  | 363776                    | 
| Capital Goods                                    | 258712                    | 
| "Food, Beverage & Tobacco"                       | 111131                    | 
| "Pharmaceuticals, Biotechnology & Life Sciences" | 72486                     | 
| Chemicals                                        | 62369                     | 
| Software & Services                              | 46544                     | 
| Media                                            | 23017                     | 


#4 What are the companies with the highest contribution to carbon emission?


SELECT  c.company_name, sum(carbon_footprint_pcf) as Carbon_Emission
FROM product_emissions p
LEFT JOIN companies as c ON c.id = p.company_id
GROUP BY 1
ORDER BY 2 desc
LIMIT 10

| company_name                            | Carbon_Emission | 
| --------------------------------------: | --------------: | 
| "Gamesa Corporación Tecnológica, S.A."  | 9778464         | 
| Daimler AG                              | 1594300         | 
| Volkswagen AG                           | 655960          | 
| "Mitsubishi Gas Chemical Company, Inc." | 212016          | 
| "Hino Motors, Ltd."                     | 191687          | 
| Arcelor Mittal                          | 167007          | 
| Weg S/A                                 | 160655          | 
| General Motors Company                  | 137007          | 
| "Lexmark International, Inc."           | 132012          | 
| "Daikin Industries, Ltd."               | 105600          | 


#5 What are the countries with the highest contribution to carbon emissions?

SELECT  c.country_name, sum(carbon_footprint_pcf) as Carbon_Emission
FROM product_emissions p
LEFT JOIN countries as c ON c.id = p.country_id
GROUP BY 1
ORDER BY 2 desc
LIMIT 10


| country_name | Carbon_Emission | 
| -----------: | --------------: | 
| Spain        | 9786130         | 
| Germany      | 2251225         | 
| Japan        | 653237          | 
| USA          | 518381          | 
| South Korea  | 186965          | 
| Brazil       | 169337          | 
| Luxembourg   | 167007          | 
| Netherlands  | 70417           | 
| Taiwan       | 62875           | 
| India        | 24574           | 

#6 What is the trend of carbon footprints (PCFs) over the years?

SELECT year,
	   sum(carbon_footprint_pcf) as total_carbon_emission,
	   round(avg(carbon_footprint_pcf),2) as avg_carbon_emission,
	   max(carbon_footprint_pcf) as max_carbon_emission
FROM product_emissions
GROUP BY 1
ORDER BY 1


| year | total_carbon_emission | avg_carbon_emission | max_carbon_emission | 
| ---: | --------------------: | ------------------: | ------------------: | 
| 2013 | 503857                | 2399.32             | 167000              | 
| 2014 | 624226                | 2457.58             | 87589               | 
| 2015 | 10840415              | 43188.90            | 3718044             | 
| 2016 | 1640182               | 6891.52             | 191687              | 
| 2017 | 340271                | 4050.85             | 99075               | 


#7 Which industry groups has demonstrated the most notable decrease in carbon footprints (PCFs) over time?

