# ToDoList

# Purpose: A easy to do list you can use to organize things you need to be done

# Instructions:
# STEP 1: Import files into apex orical
# STEP 2: Run Application
# STEP 3: go to SQL Comands and run the following code 

  CREATE TABLE "TODO"
   ("PID" NUMBER,
    "TODO" VARCHAR2("50") NOT NULL ENABLE,
    "INSERT_BY" VARCHAR2(100),
    "UPDATE_BY" VARCHAR2(100),
    "UPDATE_DATE" TIMESTAMP (6),
    "INSERT_DATE" TIMESTAMP(6),
     CONSTRAINT "TODO_PK" PRIMARY KEY ("PID")
   )

# Next go to tables select the ToDo table then select triggers, after selecting triigers go to the pk trigger thats alrad created, delete the code thats there and then compile and save this code were it was:


 create or replace TRIGGER "TODO_PK"
 
  before insert or update
  
  on TODO
  
  for each row
  
  begin
  
     if inserting then
     
       if :NEW.PID is null then
       
           select nvl(max(pid),0) + 1
           
           into :NEW.PID
           
           from TODO;
           
       end if;
       
        :NEW.INSERT_DATE := localtimestamp;
        :NEW.INSERT_BY := nvl(v('APP_USER'),USER);
    end if;

     if updating then
        :NEW.UPDATE_DATE := localtimestamp;
        :NEW.UPDATE_BY := nvl(v('APP_USER'),USER);
     end if;
     
 end;

 Credit: CodeXpertise on YouTube
