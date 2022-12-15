—-------------------------------------Populate Account Phone on Contact Phone--------------------------------------------------------------------------
trigger ContactObjectTrigger on Contact (before insert, before update) {
		
	    List<Contact> lisOfNewContact = trigger.new;
    	Set<Id> setOfAccountId = new Set<Id>();
    
            for(Contact con : lisOfNewContact){
                setOfAccountId.add(con.AccountId);
            }
    		
    		List<Account> listOfAccount = [SELECT Id, Name, Phone FROM Account WHERE Id =: setOfAccountId];
    	
            for(Contact con : lisOfNewContact){
                if(con.phone == null){
                    
                    for(Account acc : listOfAccount){
                        if(con.AccountId == acc.Id){
                            con.Phone = acc.Phone;
                        }
                    }         
                }
            }    
}
