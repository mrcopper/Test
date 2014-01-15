#!/bin/bash

npes=24
days=75

make all

if [ $? -eq 0 ] 
  then 

  time mpirun -n $npes ./torus > runlog

  if [ $? -ge 0 ] 
    then 

    mv DENS*.dat plots/.  
    mv MIXR*.dat plots/.  
    mv TEMP*.dat plots/.  
    mv INTS*.dat plots/.  
    mv intensity*.dat plots/.  

    cd plots

      ./plotify $days DENS
      mv animated.avi ../dens.avi
#      ./plotify $days INTS
#      mv animated.avi ../intensity.avi
      ./overlay $days 
      mv overlay.jpeg ../.
#      mv animated.gif ../dens.gif
#      ./plotify 150 TEMP
#      mv animated.gif ../temp.gif

      mv DENS*.dat data/.  
      mv MIXR*.dat data/.  
      mv TEMP*.dat data/.  
      mv INTS*.dat data/.  
      rm intensity*.dat

      cd data
        ./organize.sh    
        ./peakPlot.sh $days
        ./plotRatio.sh $days
        cp peaks.jpeg ../../.
        cp peakRatio.jpeg ../../.
      cd ..

    cd ..

  fi

fi

make clean

#gifview -a dens.gif &
#mplayer -loop -0 dens.avi &
vlc dens.avi &
#vlc intensity.avi &
#mplayer dens.avi &
display peaks.jpeg & 
display peakRatio.jpeg  
#display overlay.jpeg



