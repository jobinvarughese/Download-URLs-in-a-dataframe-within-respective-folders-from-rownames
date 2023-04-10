# Download-URLs-in-a-dataframe-within-respective-folders-from-rownames
This set of codes is to download URLs form the internet when they are present in a dataframe and you need to download them sequentially in their respective folders as determined by one of the columns in the dataframe

#how to download images from url and create folders based on a dataframe##
#Downloading pictures from URL into respective folders based on a dataframe  ###

#Set working directory till the folder where you want to create new folders#
setwd("/Users/jobinvarughese/Desktop/iiser/10th sem/regen paper/All veg collated/To be collated/photos/Subash2_total_w_regen/abv50")

#Then create the folders. The files with foldername in their path will not download unless there is a folder with that name
paths <- sub("/+$", "", do.call(file.path, endfoldernames)) #endfoldernames is a vector with all folder names
dirs  <- sub("(.*)/.*", "\\1", paths)
for (dir in unique(dirs)) dir.create(dir, showWarnings = FALSE, recursive = TRUE)



foldername<- Subash3_1[grepl("https", Subash3_1$Photos),]$endfoldername #to check foldernames of only the names which have the urls in them
urls<- Subash3_1[grepl("https", Subash3_1$Photos),]$Photos # collection of only urls




#Paste the http files to particular folders 

#creating names of the files based on their urls, for easy identification
names<-NA
names<- paste(siteID,"/",basename(urls),sep="",".jpg" )


#downloading the files
for(i in 1:length(urls)){
  download.file(urls[i], destfile=names[i], mode='wb')
}

