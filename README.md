Table_extraction

yolov5 yaml-> 'Table', 'Text1', 'Text2','Info', 'Picture','Text_box'클래스에 대해 각각 학습함



cnt 변수를 0으로 초기화 



cnt변수 조건 -> 검출 클래스에서 'Table'이나 'Info'가 검출이되면 검출된 갯수만큼 cnt값을 더함.  
    
    다른 클래스들('text1', 'text2', 'picture', 'text_box') cnt변수랑 관련이 없음.

    cnt 변수에 따라 파일 저장경로 세팅

    if cnt >= 2:
        save dir = Type_C  

    elif cnt == 1:
                                
        if Text2:                         # cnt가 1일 때 text2 박스가 검출되면 type B(), text2 는 두 줄 이상의 줄글
            save dir = Type_B
        else:
            save dir = Type_A
    else:
        None



크롭 조건
    
    크롭 전 검출된 클래스들의 바운딩박스 좌표 min(x),max(x), min(y), max(y) 취합 후 coord 리스트에 저장

    cnt 변수값에 따라 cnt>0 이면 크롭을 진행

    저장 경로는 위에 분류 로직에 따라 저장됨.




Fire_extraction


yolov5 yaml-> 'file' 단일 클래스에 대해 학습함

Table extraction의 로직에서 파일 분류하는 로직만 주석처리 후 크롭 조건은 동일하게 진행.







------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Project dir architecture


Type_A  ↘

Type_B 	→  Save dir for cropped files

Type_C 	↗
	
	
yolov5

	|- dataset
 	|	- File_classification
 	|			- test		- images
 	|
 	|			- train 	- images
 	|					- labels
 	|			- valid  
 	|					- images
 	|					- labels
 	|									
 	|	- Table_classification
 	|			- test		- images
 	|
 	|			- train 	- images
 	|					- labels
 	|			- valid  
 	|					- images
 	|					- labels
 	|									
 	|- runs
 	|	- detect
 	|		- exp			- detected and cropped files	
 	|		- zip_code		- exp dir to zip				- task dir file count
 	|
 	|	- train	
 	|		- general yolov5 setting	
 	|
 	|
 	|- models	- general yolov5 setting
 	|
 	|- yaml file 				(File_extraction)	"select_Star2.yaml
 	|- yaml file 				(Table_extraction)	"select_Star.yaml"
 	|
 	|- Detect file			(File_extraction)	"Detect_File_classification.ipynb"	
 	|- Detect file			(Table_extraction)	"Detect_Table_classification.ipynb"	
 	|
 	|
 	|- Train file				(File_extraction)	"train_file_classification.ipynb"
 	|- Train file				(Table_extraction)	"train_table_classification.ipynb"
	
Augmentation.ipynb
 	
  	|- random application of brightness, saturation, contrast


data_conversion.ipynb

 	|- xml to txt

   	|- looking for missing image or label file
  	
   	|- class number redefinition

	




