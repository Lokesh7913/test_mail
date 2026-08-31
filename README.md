# test_mail
CASE "VDS_Sequencing".VDS_Auto_Steps OF
        
        //=========================================================
        // DIVERTER 7
        //=========================================================
    1:
            
            IF NOT "VDS_Sequencing".Diverter_7_Healthy THEN
                "VDS_Sequencing".VDS_Auto_Steps := 4;
            ELSIF "VDS_Sequencing".Diverter_7_Healthy THEN
              
                "VDS_Sequencing".Divertor_7_Open := 0;
                
                "VDS_Sequencing".Divertor7_Close := 1;
                
                "VDS_Sequencing".VDS_Auto_Steps := 2;
            END_IF;
            
            
            2:
            
            "F_TRIG_DB_6"(CLK := "Chute 7 full sensor");
            
            IF "F_TRIG_DB_6".Q THEN
                "VDS_Sequencing".Chute_sensor_falling_set7 := 1;
            END_IF;
            
            IF "VDS_Sequencing".Chute_sensor_falling_set7 THEN
                "VDS_Sequencing".VDS_Auto_Steps := 3;
                "Timer_DB".TIMER[7]."EN" := 1;
            END_IF;
            
            
            3:
            "@TON"(
                   EN_Timer := "Timer_DB".TIMER[7]."EN",
                   Time_SP := "VDS_Sequencing".HMI_OPEN_time,
                   Edge := "1_Sec_Pulse",
                   Time_OP => "Timer_DB".TIMER[7].OP,
                   Time_ELPS := "Timer_DB".TIMER[7].Elapse_Time
            );
            
            IF "Timer_DB".TIMER[7].OP
                OR "VDS_Sequencing".Chute_Full_Diverter7 THEN
                "VDS_Sequencing".Divertor7_Close := 0;
                "VDS_Sequencing".Divertor_7_Open := 1;
                "VDS_Sequencing".Chute_sensor_falling_set7 := 0;
                "VDS_Sequencing".VDS_Auto_Steps := 4;
            END_IF;
            
            
            //=========================================================
            // DIVERTER 6
            //=========================================================
            4:
            "Timer_DB".TIMER[7]."EN" := 0;
            "Timer_DB".TIMER[7].OP := 0;
            "Timer_DB".TIMER[7].Elapse_Time := 0;
            
            IF NOT "VDS_Sequencing".Diverter_6_Healthy THEN
                "VDS_Sequencing".VDS_Auto_Steps := 7;
            ELSIF "VDS_Sequencing".Diverter_6_Healthy THEN
                
               
                "VDS_Sequencing".Divertor_6_Open := 0;
           
                
                "VDS_Sequencing".Divertor6_Close := 1;
                
                "VDS_Sequencing".VDS_Auto_Steps := 5;
                
            END_IF;
            
            
            5:
            "F_TRIG_DB_5"(CLK := "Chute 6 full sensor");
            
            IF "F_TRIG_DB_5".Q THEN
                "VDS_Sequencing".Chute_sensor_falling_set6 := 1;
            END_IF;
            
            IF "VDS_Sequencing".Chute_sensor_falling_set6 THEN
                "Timer_DB".TIMER[6]."EN" := 1;
                "VDS_Sequencing".VDS_Auto_Steps := 6;
            END_IF;
            
            
            6:
            "@TON"(
                   EN_Timer := "Timer_DB".TIMER[6]."EN",
                   Time_SP := "VDS_Sequencing".HMI_OPEN_time,
                   Edge := "1_Sec_Pulse",
                   Time_OP => "Timer_DB".TIMER[6].OP,
                   Time_ELPS := "Timer_DB".TIMER[6].Elapse_Time
            );
            
            IF "Timer_DB".TIMER[6].OP
                OR "VDS_Sequencing".Chute_Full_Diverter6 THEN
                
                "VDS_Sequencing".Divertor6_Close := 0;
                "VDS_Sequencing".Divertor_6_Open := 1;
                "VDS_Sequencing".Chute_sensor_falling_set6 := 0;
                
                "Timer_DB".TIMER[6]."EN" := 0;
                "Timer_DB".TIMER[6].OP := 0;
                "Timer_DB".TIMER[6].Elapse_Time := 0;
                
                "VDS_Sequencing".VDS_Auto_Steps := 7;
            END_IF;
            
            
            //=========================================================
            // DIVERTER 5
            //=========================================================
            7:
            "Timer_DB".TIMER[6]."EN" := 0;
            "Timer_DB".TIMER[6].OP := 0;
            "Timer_DB".TIMER[6].Elapse_Time := 0;
            
            
            IF NOT "VDS_Sequencing".Diverter_5_Healthy THEN
                "VDS_Sequencing".VDS_Auto_Steps := 10;
            ELSIF "VDS_Sequencing".Diverter_5_Healthy THEN
                
              
                "VDS_Sequencing".Divertor_5_Open := 0;
          
                
                "VDS_Sequencing".Divertor5_Close := 1;
                
                "VDS_Sequencing".VDS_Auto_Steps := 8;
                
            END_IF;
            
            
            8:
            
            "F_TRIG_DB_4"(CLK := "Chute5 full sensor");
            
            IF "F_TRIG_DB_4".Q THEN
                "VDS_Sequencing".Chute_sensor_falling_set5 := 1;
            END_IF;
            
            IF "VDS_Sequencing".Chute_sensor_falling_set5 THEN
                "Timer_DB".TIMER[5]."EN" := 1;
                "VDS_Sequencing".VDS_Auto_Steps := 9;
            END_IF;
            
            
            9:
            "@TON"(
                   EN_Timer := "Timer_DB".TIMER[5]."EN",
                   Time_SP := "VDS_Sequencing".HMI_OPEN_time,
                   Edge := "1_Sec_Pulse",
                   Time_OP => "Timer_DB".TIMER[5].OP,
                   Time_ELPS := "Timer_DB".TIMER[5].Elapse_Time
            );
            
            IF "Timer_DB".TIMER[5].OP
                OR "VDS_Sequencing".Chute_Full_Diverter5 THEN
                "VDS_Sequencing".Divertor5_Close := 0;
                "VDS_Sequencing".Divertor_5_Open := 1;
                "VDS_Sequencing".Chute_sensor_falling_set5 := 0;
                
                "Timer_DB".TIMER[5]."EN" := 0;
                "Timer_DB".TIMER[5].OP := 0;
                "Timer_DB".TIMER[5].Elapse_Time := 0;
                
                "VDS_Sequencing".VDS_Auto_Steps := 10;
            END_IF;
            
            
            //=========================================================
            // DIVERTER 4
            //=========================================================
            10:
            "Timer_DB".TIMER[5]."EN" := 0;
            "Timer_DB".TIMER[5].OP := 0;
            "Timer_DB".TIMER[5].Elapse_Time := 0;
            
            IF NOT "VDS_Sequencing".Diverter_4_Healthy THEN
                "VDS_Sequencing".VDS_Auto_Steps := 13;
            ELSIF "VDS_Sequencing".Diverter_4_Healthy THEN
                
               
                "VDS_Sequencing".Divertor_4_Open := 0;
               
                
                
                "VDS_Sequencing".Divertor4_Close := 1;
                "VDS_Sequencing".VDS_Auto_Steps := 11;
                
            END_IF;
            
            
            11:
            "F_TRIG_DB_3"(CLK := "chute 4 full sensor");
            
            IF "F_TRIG_DB_3".Q THEN
                "VDS_Sequencing".Chute_sensor_falling_set4 := 1;
            END_IF;
            
            IF "VDS_Sequencing".Chute_sensor_falling_set4 THEN
                "Timer_DB".TIMER[4]."EN" := 1;
                "VDS_Sequencing".VDS_Auto_Steps := 12;
            END_IF;
            
            
            12:
            "@TON"(
                   EN_Timer := "Timer_DB".TIMER[4]."EN",
                   Time_SP := "VDS_Sequencing".HMI_OPEN_time,
                   Edge := "1_Sec_Pulse",
                   Time_OP => "Timer_DB".TIMER[4].OP,
                   Time_ELPS := "Timer_DB".TIMER[4].Elapse_Time
            );
            
            IF "Timer_DB".TIMER[4].OP
                OR "VDS_Sequencing".Chute_Full_Diverter4 THEN
                
                "VDS_Sequencing".Divertor4_Close := 0;
                "VDS_Sequencing".Divertor_4_Open := 1;
                "VDS_Sequencing".Chute_sensor_falling_set4 := 0;
                
                "Timer_DB".TIMER[4]."EN" := 0;
                "Timer_DB".TIMER[4].OP := 0;
                "Timer_DB".TIMER[4].Elapse_Time := 0;
                
                "VDS_Sequencing".VDS_Auto_Steps := 13;
            END_IF;
            
            
            //=========================================================
            // DIVERTER 3
            //=========================================================
            13:
            "Timer_DB".TIMER[4]."EN" := 0;
            "Timer_DB".TIMER[4].OP := 0;
            "Timer_DB".TIMER[4].Elapse_Time := 0;
            
            
            IF NOT "VDS_Sequencing".Diverter_3_Healthy THEN
                "VDS_Sequencing".VDS_Auto_Steps := 16;
            ELSIF "VDS_Sequencing".Diverter_3_Healthy THEN
               
                "VDS_Sequencing".Divertor_3_Open := 0;
               
                
                "VDS_Sequencing".Divertor3_Close := 1;
                "VDS_Sequencing".VDS_Auto_Steps := 14;
                
            END_IF;
            
            
            14:
            "F_TRIG_DB_2"(CLK := "Chute 3 full sensor");
            
            IF "F_TRIG_DB_2".Q THEN
                "VDS_Sequencing".Chute_sensor_falling_set3 := 1;
            END_IF;
            
            IF "VDS_Sequencing".Chute_sensor_falling_set3 THEN
                "Timer_DB".TIMER[3]."EN" := 1;
                "VDS_Sequencing".VDS_Auto_Steps := 15;
            END_IF;
            
            
            15:
            "@TON"(
                   EN_Timer := "Timer_DB".TIMER[3]."EN",
                   Time_SP := "VDS_Sequencing".HMI_OPEN_time,
                   Edge := "1_Sec_Pulse",
                   Time_OP => "Timer_DB".TIMER[3].OP,
                   Time_ELPS := "Timer_DB".TIMER[3].Elapse_Time
            );
            
            IF "Timer_DB".TIMER[3].OP
                OR "VDS_Sequencing".Chute_Full_Diverter3 THEN
                "VDS_Sequencing".Divertor3_Close := 0;
                "VDS_Sequencing".Divertor_3_Open := 1;
                "VDS_Sequencing".Chute_sensor_falling_set3 := 0;
                
                "Timer_DB".TIMER[3]."EN" := 0;
                "Timer_DB".TIMER[3].OP := 0;
                "Timer_DB".TIMER[3].Elapse_Time := 0;
                
                "VDS_Sequencing".VDS_Auto_Steps := 16;
            END_IF;
            
            
            //=========================================================
            // DIVERTER 2
            //=========================================================
            16:
            "Timer_DB".TIMER[3]."EN" := 0;
            "Timer_DB".TIMER[3].OP := 0;
            "Timer_DB".TIMER[3].Elapse_Time := 0;
            
            
            IF NOT "VDS_Sequencing".Diverter_2_Healthy THEN
                "VDS_Sequencing".VDS_Auto_Steps := 19;
            ELSIF "VDS_Sequencing".Diverter_2_Healthy & NOT "VDS_Sequencing".Divertor_2_Open THEN
            
                "VDS_Sequencing".Divertor_2_Open := 0;
               
                
                "VDS_Sequencing".Divertor2_Close := 1;
                "VDS_Sequencing".VDS_Auto_Steps := 17;
                
            END_IF;
            
            
            17:
            "F_TRIG_DB_1"(CLK := "Chute 2 full sensor");
            
            IF "F_TRIG_DB_1".Q THEN
                "VDS_Sequencing".Chute_sensor_falling_set2 := 1;
            END_IF;
            
            IF "VDS_Sequencing".Chute_sensor_falling_set2 THEN
                "Timer_DB".TIMER[2]."EN" := 1;
                "VDS_Sequencing".VDS_Auto_Steps := 18;
            END_IF;
            
            
            18:
            "@TON"(
                   EN_Timer := "Timer_DB".TIMER[2]."EN",
                   Time_SP := "VDS_Sequencing".HMI_OPEN_time,
                   Edge := "1_Sec_Pulse",
                   Time_OP => "Timer_DB".TIMER[2].OP,
                   Time_ELPS := "Timer_DB".TIMER[2].Elapse_Time
            );
            
            IF "Timer_DB".TIMER[2].OP
                OR "VDS_Sequencing".Chute_Full_Diverter2 THEN
                "VDS_Sequencing".Divertor2_Close := 0;
                "VDS_Sequencing".Divertor_2_Open := 1;
                "VDS_Sequencing".Chute_sensor_falling_set2 := 0;
                
                "Timer_DB".TIMER[2]."EN" := 0;
                "Timer_DB".TIMER[2].OP := 0;
                "Timer_DB".TIMER[2].Elapse_Time := 0;
                
                "VDS_Sequencing".VDS_Auto_Steps := 19;
            END_IF;
            
            
            //=========================================================
            // DIVERTER 1
            //=========================================================
            19:
            "Timer_DB".TIMER[2]."EN" := 0;
            "Timer_DB".TIMER[2].OP := 0;
            "Timer_DB".TIMER[2].Elapse_Time := 0;
            
            
            IF NOT "VDS_Sequencing".Diverter_1_Healthy THEN
                "VDS_Sequencing".VDS_Auto_Steps := 1;
            ELSIF "VDS_Sequencing".Diverter_1_Healthy THEN
                "VDS_Sequencing".Divertor_1_Open := 0;
             
                
                "VDS_Sequencing".Divertor1_Close := 1;
                "VDS_Sequencing".VDS_Auto_Steps := 20;
                
            END_IF;
            
            
            20:
            "F_TRIG_DB"(CLK := "Chute 1 full sensor");
            
            IF "F_TRIG_DB".Q THEN
                "VDS_Sequencing".Chute_sensor_falling_set1 := 1;
            END_IF;
            
            IF "VDS_Sequencing".Chute_sensor_falling_set1 THEN
                "Timer_DB".TIMER[1]."EN" := 1;
                "VDS_Sequencing".VDS_Auto_Steps := 21;
            END_IF;
            
            
            21:
            "@TON"(
                   EN_Timer := "Timer_DB".TIMER[1]."EN",
                   Time_SP := "VDS_Sequencing".HMI_OPEN_time,
                   Edge := "1_Sec_Pulse",
                   Time_OP => "Timer_DB".TIMER[1].OP,
                   Time_ELPS := "Timer_DB".TIMER[1].Elapse_Time
            );
            
            IF "Timer_DB".TIMER[1].OP
                OR "VDS_Sequencing".Chute_Full_Diverter1 THEN
                "VDS_Sequencing".Divertor1_Close := 0;
                "VDS_Sequencing".Divertor_1_Open := 1;
                "VDS_Sequencing".Chute_sensor_falling_set1 := 0;
                
                "Timer_DB".TIMER[1]."EN" := 0;
                "Timer_DB".TIMER[1].OP := 0;
                "Timer_DB".TIMER[1].Elapse_Time := 0;
                
                // Sequence completed - restart from Diverter 7
                "VDS_Sequencing".VDS_Auto_Steps := 1;
            END_IF;
        
END_CASE;
        

