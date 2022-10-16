# 20221015 Notes for Sync 

Question 
1. Is the commit Okay? 
2. How to implement psudo instruction?
3. `rv->count` sould be replaced with Register `CYCLEH`, `TIMEH`, `INSTRET`?

## Performance counter implementation spec

* Add api for debugging
* Add counter++ in each cycle




Hi @jserv, 
I am not sure I am taking the correct step 

- [x] 1. Create an API for getting performance counter 
- [ ] 2. Implementing the incrementation of CSR_CYCLEH, CSR_TIME and CSR_INSTRT in `rv_step()`
