

	/* Random sample without replacement */
	data test.credit(drop = i j count good_bad);
   	count=0;
   	array obsnum(200) _temporary_;
   	do i = 1 to 200; 
    redo:
   	 	select=ceil(ranuni(12345)*n);
    	set sampsio.dmagecr point=select nobs=n;
    do j=1 to count;
      if obsnum(j)=select then goto redo;
    end;
    	count=count+1;
    	obsnum(count)=select;
    	output;
   	end; 
   	STOP;
 	run;