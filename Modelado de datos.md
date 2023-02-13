Se importan las librería que se utilizarán para el desarrollo de este ejercicio.


```python
import pandas as pd
import numpy as np
```

Se carga el conjunto de datos, se renombran sus columnas y se muestra el encabezado.


```python
datos = pd.read_csv("./salary_survey.csv")
columnas = ["FECHA", "EDAD", "INDUSTRIA", "CARGO", "CONTEXTO CARGO", "SALARIO ANUAL", "COMPENSACION", "MONEDA", "OTRA MONEDA",
            "CONTEXTO INGRESOS", "PAIS", "ESTADO USA", "CIUDAD", "EXPERIENCIA", "EXPERIENCIA CAMPO", "EDUCACION", "GENERO",
            "RAZA"]
datos.set_axis(columnas, axis = "columns", inplace = True)
datos.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>FECHA</th>
      <th>EDAD</th>
      <th>INDUSTRIA</th>
      <th>CARGO</th>
      <th>CONTEXTO CARGO</th>
      <th>SALARIO ANUAL</th>
      <th>COMPENSACION</th>
      <th>MONEDA</th>
      <th>OTRA MONEDA</th>
      <th>CONTEXTO INGRESOS</th>
      <th>PAIS</th>
      <th>ESTADO USA</th>
      <th>CIUDAD</th>
      <th>EXPERIENCIA</th>
      <th>EXPERIENCIA CAMPO</th>
      <th>EDUCACION</th>
      <th>GENERO</th>
      <th>RAZA</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4/27/2021 11:02:10</td>
      <td>25-34</td>
      <td>Education (Higher Education)</td>
      <td>Research and Instruction Librarian</td>
      <td>NaN</td>
      <td>55,000</td>
      <td>0.0</td>
      <td>USD</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>United States</td>
      <td>Massachusetts</td>
      <td>Boston</td>
      <td>5-7 years</td>
      <td>5-7 years</td>
      <td>Master's degree</td>
      <td>Woman</td>
      <td>White</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4/27/2021 11:02:22</td>
      <td>25-34</td>
      <td>Computing or Tech</td>
      <td>Change &amp; Internal Communications Manager</td>
      <td>NaN</td>
      <td>54,600</td>
      <td>4000.0</td>
      <td>GBP</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>United Kingdom</td>
      <td>NaN</td>
      <td>Cambridge</td>
      <td>8 - 10 years</td>
      <td>5-7 years</td>
      <td>College degree</td>
      <td>Non-binary</td>
      <td>White</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4/27/2021 11:02:38</td>
      <td>25-34</td>
      <td>Accounting, Banking &amp; Finance</td>
      <td>Marketing Specialist</td>
      <td>NaN</td>
      <td>34,000</td>
      <td>NaN</td>
      <td>USD</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>US</td>
      <td>Tennessee</td>
      <td>Chattanooga</td>
      <td>2 - 4 years</td>
      <td>2 - 4 years</td>
      <td>College degree</td>
      <td>Woman</td>
      <td>White</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4/27/2021 11:02:41</td>
      <td>25-34</td>
      <td>Nonprofits</td>
      <td>Program Manager</td>
      <td>NaN</td>
      <td>62,000</td>
      <td>3000.0</td>
      <td>USD</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>USA</td>
      <td>Wisconsin</td>
      <td>Milwaukee</td>
      <td>8 - 10 years</td>
      <td>5-7 years</td>
      <td>College degree</td>
      <td>Woman</td>
      <td>White</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4/27/2021 11:02:42</td>
      <td>25-34</td>
      <td>Accounting, Banking &amp; Finance</td>
      <td>Accounting Manager</td>
      <td>NaN</td>
      <td>60,000</td>
      <td>7000.0</td>
      <td>USD</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>US</td>
      <td>South Carolina</td>
      <td>Greenville</td>
      <td>8 - 10 years</td>
      <td>5-7 years</td>
      <td>College degree</td>
      <td>Woman</td>
      <td>White</td>
    </tr>
  </tbody>
</table>
</div>



Se remueven las comas de los valores de la columna *Salario anual*.


```python
datos["SALARIO ANUAL"] = pd.to_numeric(datos["SALARIO ANUAL"].replace(',', '', regex = True))
```

Se filtran los registros que tengan un salario anual mayor que *1000000* y moneda *USD*, y se ordena la tabla de forma descendente por el *Salario anual*.


```python
datos.loc[(datos["SALARIO ANUAL"] > 1000000) &
          (datos["SALARIO ANUAL"] == "USD")].sort_values("SALARIO ANUAL", ascending = False)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>FECHA</th>
      <th>EDAD</th>
      <th>INDUSTRIA</th>
      <th>CARGO</th>
      <th>CONTEXTO CARGO</th>
      <th>SALARIO ANUAL</th>
      <th>COMPENSACION</th>
      <th>MONEDA</th>
      <th>OTRA MONEDA</th>
      <th>CONTEXTO INGRESOS</th>
      <th>PAIS</th>
      <th>ESTADO USA</th>
      <th>CIUDAD</th>
      <th>EXPERIENCIA</th>
      <th>EXPERIENCIA CAMPO</th>
      <th>EDUCACION</th>
      <th>GENERO</th>
      <th>RAZA</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>



De la tabla anterior, se puede observar que hay una persona que tiene un salario anual de *102000000* de unidades monetarias. También, se puede apreciar que la otra moneda es *COP*, por lo que pareciera que dicho valor es en pesos colombianos y no en dólares.

Se cambia COP por USD en el campo *Moneda* del índice 3605, el cual es la persona que recibe más de cien millones de unidades monetarias.


```python
datos.loc[3605, "MONEDA"] = "Other"
```

Se remplazan todos los valores *nan* por 0.


```python
datos["COMPENSACION"] = datos["COMPENSACION"].fillna(0)
```

Se quitan los espacios en blanco y se convierten en mayúsculas los datos de la columna *País* y *Ciudad*.


```python
datos["PAIS"] = datos["PAIS"].str.strip().str.upper()
datos["CIUDAD"] = datos["CIUDAD"].str.strip().str.upper()
```

Se identifican los países que tienen más de un nombre con el objetivo de unificarlos en uno solo.


```python
lista_AUSTRALIA = ["AUSTRALI", "AUSTRALIAN"]
lista_BRAZIL = ["BRASIL"]
lista_CANADA = ["CAN", "CANAD", "CANADA, OTTAWA, ONTARIO", "CANADW", "CANADÁ", "CANDA", "CSNADA", "POLICY"]
lista_CHANNEL_ISLANDS = ["JERSEY, CHANNEL ISLANDS"]
lista_CHINA = ["HONG KONG", "HONG KONH", "MAINLAND CHINA"]
lista_CZECH_REPUBLIC = ["CZECHIA", "EUROPE"]
lista_DENMARK = ["DANMARK"]
lista_ITALY = ["ITALY (SOUTH)"]
lista_IVORY_COAST = ["COTE D'IVOIRE"]
lista_JAPAN = ["JAPAN, US GOV POSITION"]
lista_LUXEMBOURG = ["LUXEMBURG"]
lista_MEXICO = ["MÉXICO"]
lista_NETHERLANDS = ["NEDERLAND", "NL", "THE NETHERLANDS"]
lista_NEW_ZEALAND = ["AOTEAROA NEW ZEALAND", "FROM NEW ZEALAND BUT ON PROJECTS ACROSS APAC", "NEW ZEALAND AOTEAROA", "NZ"]
lista_PANAMA = ["PANAMÁ"]
lista_SPAIN = ["CATALONIA"]
lista_UNITED_ARAB_EMIRATES = ["UAE"]
lista_UNITED_KINGDOM = ["BRITAIN",
                        "ENGLAND",
                        "ENGLAND, GB",
                        "ENGLAND, UK",
                        "ENGLAND, UK.",
                        "ENGLAND, UNITED KINGDOM",
                        "ENGLAND/UK",
                        "ENGLANG",
                        "GREAT BRITAIN",
                        "NORTHERN IRELAND",
                        "NORTHERN IRELAND, UNITED KINGDOM",
                        "SCOTLAND",
                        "SCOTLAND, UK",
                        "U.K",
                        "U.K.",
                        "U.K. (NORTHERN ENGLAND)",
                        "UK",
                        "UK (ENGLAND)",
                        "UK (NORTHERN IRELAND)",
                        "UK, BUT FOR GLOBALLY FULLY REMOTE COMPANY",
                        "UK, REMOTE",
                        "UNITED KINDOM",
                        "UNITED KINGDOM (ENGLAND)",
                        "UNITED KINGDOM.",
                        "UNITED KINGDOMK",
                        "UNITES KINGDOM",
                        "WALES",
                        "WALES (UK)",
                        "WALES (UNITED KINGDOM)",
                        "WALES, UK"]
lista_UNITED_STATES = ["AMERICA",
                       "BONUS BASED ON MEETING YEARLY GOALS SET W/ MY SUPERVISOR",
                       "CALIFORNIA",
                       "CONTRACTS",
                       "CURRENTLY FINANCE",
                       "FOR THE UNITED STATES GOVERNMENT, BUT POSTED OVERSEAS",
                       "HARTFORD",
                       "I AM LOCATED IN CANADA BUT I WORK FOR A COMPANY IN THE US",
                       "I EARN COMMISSION ON SALES. IF I MEET QUOTA, I'M GUARANTEED ANOTHER 16K MIN. LAST YEAR I EARNED AN ADDITIONAL 27K. IT'S NOT UNCOMMON FOR PEOPLE IN MY SPACE TO EARN 100K+ AFTER COMMISSION.",
                       "I WORK FOR A UAE-BASED ORGANIZATION, THOUGH I AM PERSONALLY IN THE US.",
                       "I.S.",
                       "IS",
                       "ISA",
                       "SAN FRANCISCO",
                       "THE UNITED STATES",
                       "THE US",
                       "U. S",
                       "U. S.",
                       "U.A.",
                       "U.S",
                       "U.S.",
                       "U.S.A",
                       "U.S.A.",
                       "U.S>",
                       "U.SA",
                       "UA",
                       "UK FOR U.S. COMPANY",
                       "UNIITED STATES",
                       "UNITE STATES",
                       "UNITED  STATES",
                       "UNITED SATES",
                       "UNITED SATES OF AMERICA",
                       "UNITED STARES",
                       "UNITED STATE",
                       "UNITED STATEA",
                       "UNITED STATED",
                       "UNITED STATEDS",
                       "UNITED STATEES",
                       "UNITED STATE OF AMERICA",
                       "UNITED STATES (I WORK FROM HOME AND MY CLIENTS ARE ALL OVER THE US/CANADA/PR",
                       "UNITED STATES IS AMERICA",
                       "UNITED STATES OF AMERICA",
                       "UNITED STATES OF AMERICAN",
                       "UNITED STATES OF AMERICAS",
                       "UNITED STATES- PUERTO RICO",
                       "UNITED STATESP",
                       "UNITED STATEW",
                       "UNITED STATSS",
                       "UNITED STATTES",
                       "UNITED STATUES", "UNITED STATUS",
                       "UNITED STATWS",
                       "UNITED STTES",
                       "UNITED Y",
                       "UNITEDSTATES",
                       "UNITEED STATES",
                       "UNITEF STATED",
                       "UNITER STATEZ",
                       "UNITES STATES",
                       "UNITIED STATES",
                       "UNIYED STATES",
                       "UNIYES STATES",
                       "UNTED STATES",
                       "UNTIED STATES",
                       "US",
                       "US OF A",
                       "USA",
                       "USA-- VIRGIN ISLANDS",
                       "USA (COMPANY IS BASED IN A US TERRITORY, I WORK REMOTE)",
                       "USA, BUT FOR FOREIGN GOV'T",
                       "USA TOMORROW",
                       "USAA",
                       "USAB",
                       "USAT",
                       "USD",
                       "USS",
                       "UXZ",
                       "VIRGINIA",
                       "WE DON'T GET RAISES, WE GET QUARTERLY BONUSES, BUT THEY PERIODICALLY ASSES INCOME IN THE AREA YOU WORK, SO I GOT A RAISE BECAUSE A 3RD PARTY ASSESSMENT SHOWED I WAS PAID TOO LITTLE FOR THE AREA WE WERE LOCATED",
                       "WORLDWIDE (BASED IN US BUT SHORT TERM TRIPS AROUDN THE WORLD)",
                       "Y",
                       "🇺🇸"]
lista_NA = ["$2,175.84/YEAR IS DEDUCTED FOR BENEFITS",
            "AFRICA",
            "ARGENTINA BUT MY ORG IS IN THAILAND",
            "AUSTRIA, BUT I WORK REMOTELY FOR A DUTCH/BRITISH COMPANY",
            "CANADA AND USA",
            "COMPANY IN GERMANY. I WORK FROM PAKISTAN.",
            "FROM ROMANIA, BUT FOR AN US BASED COMPANY",
            "GLOBAL",
            "I WAS BROUGHT IN ON THIS SALARY TO HELP WITH THE EHR AND VERY QUICKLY WAS PROMOTED TO CURRENT POSITION BUT COMPENSATION WAS NOT ALTERED.",
            "I WORK FOR AN US BASED COMPANY BUT I'M FROM ARGENTINA.",
            "INTERNATIONAL",
            "N/A (REMOTE FROM WHEREVER I WANT)",
            "NA",
            "REMOTE",
            "REMOTE (PHILIPPINES)",
            "US GOVT EMPLOYEE OVERSEAS, COUNTRY WITHHELD"]

lista = [lista_AUSTRALIA, lista_BRAZIL, lista_CANADA, lista_CHANNEL_ISLANDS, lista_CHINA, lista_CZECH_REPUBLIC, lista_DENMARK,
         lista_ITALY, lista_IVORY_COAST, lista_JAPAN, lista_LUXEMBOURG, lista_MEXICO, lista_NETHERLANDS, lista_NEW_ZEALAND,
         lista_PANAMA, lista_SPAIN, lista_UNITED_ARAB_EMIRATES, lista_UNITED_KINGDOM, lista_UNITED_STATES, lista_NA]
lista_paises = ["AUSTRALIA", "BRAZIL", "CANADA", "CHANNEL ISLANDS", "CHINA", "CZECH REPUBLIC", "DENMARK", "ITALY",
                "IVORY COAST", "JAPAN", "LUXEMBOURG", "MEXICO", "NETHERLANDS", "NEW ZEALAND", "PANAMA", "SPAIN",
                "UNITED ARAB EMIRATES", "UNITED KINGDOM", "UNITED STATES", ""]
for i, j in zip(lista, lista_paises):
    datos["PAIS"] = datos["PAIS"].replace(i, j)
```

Se crea una lista llamada *industria*, la cual contiene las industrias que están en la encuesta. Esto se hace con el fin de poder identificar las industrias que no están dentro de la lista previamente creada y reemplazarlas por *Other*. Esto ayuda a que no se tengan muchos datos distintos en dicha columna y a visualizar mejor su información.


```python
industria = ["Accounting, Banking & Finance",
"Agriculture or Forestry",
"Art & Design",
"Business or Consulting",
"Computing or Tech",
"Education (Primary/Secondary)",
"Education (Higher Education)",
"Engineering or Manufacturing",
"Entertainment",
"Government and Public Administration",
"Health care",
"Hospitality & Events",
"Insurance",
"Law",
"Law Enforcement & Security",
"Leisure, Sport & Tourism",
"Marketing, Advertising & PR",
"Media & Digital",
"Nonprofits",
"Property or Construction",
"Recruitment or HR",
"Retail",
"Sales",
"Social Work",
"Transport or Logistics",
"Utilities & Telecommunications"]

datos["INDUSTRIA"] = datos["INDUSTRIA"].apply(lambda i: i if i in industria else "Otro")
```

Se cambian los valores de la variable género que no sean *Man*, *Woman* o *Non-binary* por *nan*.


```python
datos["GENERO"] = datos["GENERO"].replace(["Other or prefer not to answer", "Prefer not to answer"], "Other")
datos["GENERO"] = datos["GENERO"].fillna("Other")
```

Se exporta la base de datos como un libro de Excel.


```python
datos.to_excel("Ingresos.xlsx", index = False)
```
