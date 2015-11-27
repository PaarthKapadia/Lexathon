.data

.text
	#Insert Random Number Generation Method Here
	
	#Insert Method To Generate List of Possible Words Here
	
	#Insert Method To Print Out The Letters and Prompt User to enter words
	
	li  $v0, 30			#Get system time
	syscall
    
	add $s0, $a0, $0		#Save system time
	
	#Each time the user enters a word, get system time and see if we have exceeded total time limit.  Also see if the word is valid
	
	#Keep Looping the user input part until time is up

	j Exit				#Exits program
word_Valid: # loop to check if the word is valid
	lb $t3, ($a0) 
	beq $t3, $s4,valid  #$t3 = current character, $s4 = saved characters
	bne $t3, $s4, notValid
	addi $t3, $t3, 1  # increments each letter to move onto the next one
	j word_Valid
 
 valid: # valid input. 
 	jr $ra
 
 notValid: #returns to the next word if the word is not valid
 	addi $a2,$a2,1 # goes to the next word. 
 
# Function to check if the middle letter is included
counter: # loads 0 to $a2 for the counter to be incremented
	li $a2, 0 
MiddleLetter:
	lb $t1, ($a2)
        bne $t1, $t5, NoMiddleLetter # go to NoMiddleLetter subroutine. # $t1 = middle letter #t5 = the current letter
        beq $t1, $t5, MiddleLetterExists 
        addi $a2, $a2, 1 #increment regardless of the outcome
	j counter
NoMiddleLetter:
	
MiddleLetterExists:
	jr $ra
	
Search:	#a0 is the location of the null terminated string to search for.  #a1 is the location of the beginning of all of array to search     #Returns 1 if found, 0 if not found
	subi $sp, $sp, 12
	sw $a0, ($sp)
	sw $a1, 4($sp)
	sw $ra, 8($sp)
	
Search2:
	jal CompareBytes
	bne $v0, $0, Found
	lw $a0, 4($sp)
	jal MoveArray
	sw $v0, 4($sp)
	add $a0, $v0, $0
	jal CheckEnd
	beq $v0, $0, EndOfArray
	lw $a0, ($sp)
	lw $a1, 4($sp)
	j Search2
	
EndOfArray:	
	li $v0, 0x00000000
	lw $ra, 8($sp)
	addi $sp, $sp, 12
	jr $ra
Found:	
	lw $ra, 8($sp)
	add $v0, $0, 1
	addi $sp, $sp, 12
	jr $ra
	
CompareBytes:	
	li $t9, 0x00000000
CBLoop:	lb $t0, ($a0)
	lb $t1, ($a1)
	bne $t0, $t1, NotMatch
	beq $t0, $t9, Match
	addi $a0, $a0, 1
	addi $a1, $a1, 1
	j CBLoop
Match:	
	addi $v0, $0, 1
	jr $ra
NotMatch:	
	add $v0, $0, $0
	jr $ra
	
MoveArray:	
	li $t0, 0x00000060
	li $t1, 0x0000007a
	lb $t3, ($a0)
	blt $t3, $t0, ReachedNull
	bgt $t3, $t1, ReachedNull
	addi $a0, $a0, 1
	j MoveArray	
ReachedNull:
	addi $v0, $a0, 1
	jr $ra
	
CheckEnd:
	li $t0, 0x00000060
	li $t1, 0x0000007a
	lb $t3, ($a0)
	blt $t3, $t0, IsEnd
	bgt $t3, $t1, IsEnd
	addi $v0, $0, 1
	jr $ra
IsEnd:	add $v0, $0, $0
	jr $ra
	
Exit:
