# composite-forward-swept-wing-for-transport-aircraft
structure modelling and  analysis by IPDL language in ANSYS plat form
FINISH
/CLEAR
/PREP7
/UNITS,SI
/UIS,MSGPOP,3                            					          !±íÊ¾Ö»ÏÔÊ¾´íÎóÐÅÏ¢
/VIEW,1,2,2,1     


ET,1,SHELL99                         !¶¨Òåµ¥ÔªÀàÐÍ
KEYOPT,1,8,1
R,1,10,1                             !¶¨ÒåÊµ³£Êý
RMORE
RMORE,1,  0,0.0005,1, 45,0.0007            !¶¨ÒåÆÌ²ãÐÅÏ¢  
RMORE,1, 90,0.0008,1,-45,0.0009
RMORE,1, 90,0.0010
!s
MP,EX,1,181E9                        !¶¨Òå²ÄÁÏÌØÐÔ
MP,EY,1,10.3E9
MP,EZ,1,10.3E9
MP,PRXY,1,0.016
MP,GXY,1,7.17E9
MP,GXZ,1,7.17E9
MP,GYZ,1,3.78E9
                       					          !¶¨ÒåÏÔÊ¾·½ÏòÎª(2,2,1)£¬È±Ê¡Îª(0,0,1)

!
!------------- ³õÊ¼²ÎÊý¶¨Òå ---------------------------------
!
*DIM,PARA,ARRAY,1,2                     					           
*VREAD,PARA(1,1),'WINGGRID','DAT',,JIK,2,1,1,2
(35X,F3.0,12X,F3.0)

N_Keypoints  = PARA(1,1)                 					         
N_Sections   = PARA(1,2)                 					          
NKP          = N_Sections*N_Keypoints    					          
NK           = N_Keypoints

*DIM,FPARA,ARRAY,1,2                     					          
*VREAD,FPARA(1,1),'WINGFORCE','DAT',,JIK,2,1,1,2
(35X,F3.0,12X,F3.0)

N_FKeypoints = FPARA(1,1)                					           
N_FSections  = FPARA(1,2)                					         
NFKP         = N_FSections*N_FKeypoints  					          

DENS_AL      = 2.7E3                     					          

! -----------------------------------------------------------------------------
!                                 ¹¹Ôì»úÒíÄ£ÐÍ 
! -----------------------------------------------------------------------------

!
! ------------ ¶ÁÈë»úÒí±íÃæÍø¸ñµã ---------------------------
!
*DIM,GRID,ARRAY,NKP,3
*VREAD,GRID(1,1),'WINGGRID','DAT',,JIK,3,NKP,1,3
(1X,3F12.5)
*DO,I,1,N_Sections
  *DO,J,1,N_Keypoints
    NUM  = (I-1)*N_Keypoints+J
    K,NUM,GRID(NUM,1),GRID(NUM,2),GRID(NUM,3)
  *ENDDO
*ENDDO
KPLOT
KLIST

!
! ------------ ½¨Á¢Ç°/ºóÁº¸¹°å¸ß¶ÈÏß -----------------------------------
!

NUMSTR,LINE,1                              
NUMSTR,AREA,1                             					 
*DO,I,1,N_Sections
  L,71+NK*(I-1),131+NK*(I-1)
*ENDDO

NUMSTR,LINE,101
NUMSTR,AREA,101
*DO,I,1,N_Sections
  L,41+NK*(I-1),161+NK*(I-1)
*ENDDO

!
! ------------ Éú³ÉÒíÐÍÆÊÃæÏß ------------------------------------------
!
NUMSTR,LINE,1001                                        
*DO,I,1,N_Sections
  BSPLIN,1+NK*(I-1),2+NK*(I-1),3+NK*(I-1),4+NK*(I-1),5+NK*(I-1),6+NK*(I-1)                   
  *REPEAT,20,5,5,5,5,5,5  
  BSPLIN,101+NK*(I-1),102+NK*(I-1),103+NK*(I-1),104+NK*(I-1),105+NK*(I-1),106+NK*(I-1)                   
  *REPEAT,19,5,5,5,5,5,5
  BSPLIN,196+NK*(I-1),197+NK*(I-1),198+NK*(I-1),199+NK*(I-1),200+NK*(I-1)                   
  BSPLIN,200+NK*(I-1),1+NK*(I-1)
*ENDDO
!
! ------------ Áº¸¹°åÃæ ------------------------------------------------
!
NUMSTR,LINE,1
NUMSTR,AREA,1
*DO,I,1,N_Sections-1
  ASKIN,I,I+1
*ENDDO

NUMSTR,LINE,101
NUMSTR,AREA,101
*DO,I,1,N_Sections-1
  ASKIN,100+I,101+I
*ENDDO
!
! ------------ ÒíÀßÃæ ----------------------------------------------
!
NUMSTR,LINE,501
*DO,I,1,N_Sections
  L,21+NK*(I-1),181+NK*(I-1)
  L,56+NK*(I-1),146+NK*(I-1)
  L,86+NK*(I-1),116+NK*(I-1)
*ENDDO

NUMSTR,AREA,1001
*DO,I,1,N_Sections
  AL,1001+41*(I-1),1002+41*(I-1),1003+41*(I-1),1004+41*(I-1), 501+ 3*(I-1),1037+41*(I-1),1038+41*(I-1),1039+41*(I-1),1040+41*(I-1),1041+41*(I-1)
  AL, 501+ 3*(I-1),1005+41*(I-1),1006+41*(I-1),1007+41*(I-1),1008+41*(I-1), 101+ 1*(I-1),1033+41*(I-1),1034+41*(I-1),1035+41*(I-1),1036+41*(I-1)
  AL, 101+ 1*(I-1),1009+41*(I-1),1010+41*(I-1),1011+41*(I-1), 502+ 3*(I-1),1030+41*(I-1),1031+41*(I-1),1032+41*(I-1)
  AL, 502+ 3*(I-1),1012+41*(I-1),1013+41*(I-1),1014+41*(I-1),   1+ 1*(I-1),1027+41*(I-1),1028+41*(I-1),1029+41*(I-1)
  AL,   1+ 1*(I-1),1015+41*(I-1),1016+41*(I-1),1017+41*(I-1), 503+ 3*(I-1),1024+41*(I-1),1025+41*(I-1),1026+41*(I-1)
  AL, 503+ 3*(I-1),1018+41*(I-1),1019+41*(I-1),1020+41*(I-1),1021+41*(I-1),1022+41*(I-1),1023+41*(I-1)
*ENDDO 
!
! ------------ Éú³ÉÉÏ¡¢ÏÂÒíÃæÃÉÆ¤ --------------------------------------
!

NUMSTR,LINE,1501                                            !ÏÂÒíÃæÃÉÆ¤
NUMSTR,AREA,1501
*DO,I,1,N_Sections-1                                       
  ASKIN,1001+41*(I-1),1042+41*(I-1)
  *REPEAT,20,1,1
*ENDDO 

NUMSTR,LINE,2501                                            !ÉÏÒíÃæÃÉÆ¤
NUMSTR,AREA,2501
*DO,I,1,N_Sections-1                                      
  ASKIN,1021+41*(I-1),1062+41*(I-1)
  *REPEAT,20,1,1
  ASKIN,1041+41*(I-1),1081+41*(I-1)
*ENDDO 
!   
!
 ESIZE,0.2
! 
!
! ------------ »®·ÖÃæÍø¸ñ -----------------------------------
!
    ASEL,all             !S,,,1,9999
	  TYPE,1
	  MAT,1
	  MSHKEY,2
	  AMESH,ALL
!  
LSEL,S,,,1001,1041
DL,ALL,,ALL,0  

  
/SOLU

!
! ------------ ¶ÁÈë»úÒí±íÃæÁ¦·Ö²¼ ---------------------------
!
*DIM,FORCE,ARRAY,NFKP,6
*VREAD,FORCE(1,1),'WINGFORCE','DAT',,JIK,6,NFKP,1,3
(1X,6F15.6)

NSEL,ALL
DOFSEL,ALL
*DIM,FNODE,ARRAY,NFKP,1
*DO,I,1,NFKP
  FNODE(I)  = NODE(FORCE(I,1),FORCE(I,2),FORCE(I,3))
  FCUM,ADD,1,1
  F,FNODE(I),FX,FORCE(I,4)
  FCUM,ADD,1,1
  F,FNODE(I),FY,FORCE(I,5)
  FCUM,ADD,1,1
  F,FNODE(I),FZ,FORCE(I,6)
*ENDDO
!


SOLVE
FINISH
  
  
  
  
  
  
