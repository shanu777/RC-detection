# RC-detection
Directly reading the image with ocr was giving very jumbled information with very little pattern. So, below are the steps I have used: -
1)	Fixed the skew of images.
2)	Trained yolo to detect the region of interest
3)	While extracting the area of interest from the images I intentionally enlarged the bounding box size, because the dataset was limited so model was not very accurate but it was close to the are of interest so if we enlarge the bounding box that ensures that region we are interested in gets captured.
4)	Used opencv to crop the area of interest.
5)	Ran preprocessing on images. 
6)	Converted the image data to text data using pytesseract.
7)	Used patterns to find relevant information.
8)	Converted data to pandas dataframe and saved as excel. 
Patterns:
Registration number 
•	“pattern1=r'.......\d{4}” since it always ends 4 numbers at the end.
Name
•	Removed all the common words such as ‘NAME’,’MR.’, Etc.
•	“pattern=r'[A-Z]+ [A-Z]+'”, Since the names were all capitalized and mostly consisted of first and last name I used this pattern, which extracts all the words which are capitalized.
•	Imputed the empty list with ‘Missing’.
•	Removed every word which appeared after the second word as mentioned in step 2 that names mostly consist of only 2 words.
•	Converted the nested list to a single list.
Engine Number
•	Removed all the words which were occurring commonly.
•	pattern=r'[^\W+]+' to remove the punctuation and spaces.
•	Since engine number did not follow any fixed pattern, but most of the engine numbers were above 10 digits long so I removed all the words which were smaller than 10. 
•	Because of larger bounding box we also captured chassis number and to filter chassis number I deleted the string at 1st pos because in the rc chassis number appears first and then engine number comes.
•	Imputation of empty lists with ‘Missing’ and converting nested list to single list.

Chassis Number
•	Same steps as Engine number with difference in step 3, instead of 10 I used 15.

Registration Date.
•	Replaced all the month names with corresponding number. 
•	pattern=r'\d{2}/\d{2}/\d{4}', to extract the dates. 
•	Imputation of empty lists with ‘Missing’ and converting nested list to single list.

Manufacturing Date. 
•	pattern=r'\d{2}/\d{4}', pattern2=r'\d{2}/\d{2}/\d{4}' used 2 patterns to retrieve the dates and saved them in a single list to maintain the integrity of data.
