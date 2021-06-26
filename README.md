# Web-Scraping
Hi, perkenalkan saya Galuh. Sintaks ini adalah sintaks untuk web scraping menggunakan R atau RStudio. Silakan dimodifikasi sesuai kebutuhan :)
library(httr)
library(openxlsx)
library(XML)

# Define certicificate file
cafile <- system.file("CurlSSL", "cacert.pem", package = "RCurl")

page <- GET("https://satudata.dinkop-umkm.jatengprov.go.id/",
  path="data/koperasi-kabkota/Kota%20Tegal",
  query="",
  config(cainfo = cafile)
)

# Use regex to extract the desired table
x <- text_content(page)
tab <- sub('.*(<table class="grid".*?>.*</table>).*', '\\1', x)

# Parse the table
UMKM<-readHTMLTable(tab)
UMKM #check table

# Save table
#dataframe 
df<-data.frame(UMKM)
write.xlsx(df, "path/NamaFile.xlsx")
