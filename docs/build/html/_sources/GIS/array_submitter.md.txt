```bash
if [ x$SGE_ROOT = x ]; then
   SGE_ROOT=/usr/SGE
fi
if [ ! -d $SGE_ROOT ]; then
   echo "error: SGE_ROOT directory $SGE_ROOT does not exist"
   exit 1
fi

ARC=`$SGE_ROOT/util/arch`

QSUB=$SGE_ROOT/bin/$ARC/qsub
QALTER=$SGE_ROOT/bin/$ARC/qalter

if [ ! -x $QSUB ]; then
   echo "error: cannot execute qsub command under $QSUB"
   exit 1
fi

if [ ! -x $QALTER ]; then
   echo "error: cannot execute qalter command under $QALTER"
   exit 1
fi

tasks=0

while [ "$1" != "" ]; do
   case "$1" in
   [0-9]*)
      tasks=$1
      shift
      ;;
   esac
done

if [ $tasks = 0 ]; then
   echo "usage: array_submitter.sh <number_of_tasks>"
   exit 1
fi

# submit step A jobarray
jobid_a=`$QSUB -t 1-$tasks -r y -N StepA $SGE_ROOT/examples/jobs/step_A_array_submitter.sh | cut -f3 -d" "|cut -f1 -d.`
echo "submission result: jobid_a = $jobid_a"

# submit step B jobarray with hold state
jobid_b=`$QSUB -t 1-$tasks -h -r y -N StepB $SGE_ROOT/examples/jobs/step_B_array_submitter.sh | cut -f3 -d" "|cut -f1 -d.`
echo "submission result: jobid_b = $jobid_b"

# put jobid of step B into context of step A
$QALTER -ac succ=$jobid_b $jobid_
```
