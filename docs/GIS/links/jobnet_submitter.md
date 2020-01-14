```bash
QSUB=$SGE_ROOT/bin/$ARC/qsub
name_base=Net
hold=""
jobs=5

while [ "$1" != "" ]; do
   case "$1" in
   -N)
      shift
      name_base=$1
      shift
      ;;
   -h)
      hold=-h
      shift
      ;;
   [0-9]*)
      jobs=$1
      shift
      ;;
   esac
done

echo "going to submit $jobs jobs"

jobid=0
REQUEST=""

i=1
while [ $i -le $jobs ]; do
   if [ $i -ne 1 ]; then
      opt="-hold_jid $jobid"
   fi

   jobid=`$QSUB $REQUEST -r y -N $name_base$i $hold $opt $SGE_ROOT/examples/jobs/sleeper.sh 10 | cut -f3 -d" "`
   if [ $i -ne 1 ]; then
      echo submitted job \#$i name = $name_base$i with jobid $jobid and $opt
   else
      echo submitted job \#$i name = $name_base$i with jobid $jobid
   fi
   i=`expr $i + 1`
done
```
