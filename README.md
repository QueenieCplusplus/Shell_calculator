# Shell_calculator
to call function file in script

* Script

      #! /bin/bash
      # calculate-- kind of bc-alike tool

       scale=2

      show_help()
      {

         #(a)
        cat << EOF 
          a % b ＝餘數
          a ^ b ＝a 的 b 次方
          l(x)x ＝10 的 x 次方
          e(x) ＝ e 的 x 次方
          scale N ＝小數取兩位（預設為 2）
      EOF

      }


      if [ $# -gt 0 ]; then

        exec scriptbc "$@" 

      fi 

      echo "calculate-- help or quit?"

      /bin/echo -n "calculate> "  #(b)


      while read cmd args # param is called cmd and args # (c) 
      do

         case  $cmd
         in

            quit | exit ) exit ;;
            help | ? )  show_help ;;
            scale ) scale=$args ;;
            * ) scriptbc -p $scale "$cmd" "$args" ;; 

         esac

         /bin/echo -n "calculate> "

      done


      echo " "

      exit 0 

* Syntax

   * (a) 
   
   
         cat << EOF   
   
         EOF
   
   * (b)
       
         /bin/echo -n ""
         
   * (c) while-read loop
   
* Function File called scriptbc

           先確認 Path 目錄中 scriptbc 變數有指定路徑。
           腳本以互動方式執行，如執行時指定參數，這些參數會轉轉給函式檔案做處理。

* Execution

       ✗ cd desktop
       
      ➜  desktop zsh 521a.sh
      
      calculate-- help or quit?
      calculate> help

          a % b ＝餘數
          a ^ b ＝a 的 b 次方
          l(x)x ＝10 的 x 次方
          e(x) ＝ e 的 x 次方
          scale N ＝小數取兩位（預設為 2）
          
      calculate> ^D
      521a.sh:42: command not found: scriptbc
      
      calculate> d6
      521a.sh:42: command not found: scriptbc
      
      calculate> quit
      ➜  desktop 
   
