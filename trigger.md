trigger ReturnRequestTrigger on Return_Request__c (before update) {
    for(Return_Request__c rr : Trigger.new)

    {
        Return_Request__c oldrr =  Trigger.oldMap.get(rr.Id);
         if (rr.Status__c == 'Approved' &&oldRR.Status__c != 'Approved') {
            rr.Finance_Approval__c = 'Pending';
        }
        
    }
}
