# Daily
<form action="Daily.php"method="post">

Date <input type="datetime-local" name="date"> <br>
Time arrived <input type="time" name="time_arr"> <br>
Time gone <input type="time" name="time_gone"> <br>

<button>Hisobla</button>

</form>


<?php



class Daily
{
    const  WORK_DURATION = 540;

    public DateTime $date;
    public DateTime $arrivedAt;
    public DateTime $leavedAt;

    

    public function calculate(
        string $date,
        string $leavedAt,
        string $arrivedAt
    ) {
        $arrivedAt = new DateTime($arrivedAt);
        $leavedAt = new DateTime($leavedAt);

        $dailyWorkingHours = $leavedAt->diff($arrivedAt);

        $formatted_D_workingHours = $dailyWorkingHours->format('%H %I %S');
        
        $hour = substr($formatted_D_workingHours,0,2);
        $minute = substr($formatted_D_workingHours,3,2);
        $sekund = substr($formatted_D_workingHours,6,2);
        
        $collect = (($hour * 3600) + ($minute *60) + $sekund) - 32400;
        
        $fHour = floor($collect / 3600);
        $collect %= 3600;
        $fMinute = floor($collect /60);
        $collect %= 60; 
        $fSekund = $collect;

        echo "              QARZDORLIK! \n $fHour  soat \n $fMinute  minut \n $fSekund  sekund  ";
    }
}

$today = new Daily();
$today->calculate("20.06.2024", $_POST["time_arr"], $_POST["time_gone"]);
