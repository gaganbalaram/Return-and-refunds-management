trigger AutoPendingStatusTrigger on Return_Request__c (before insert, before update) {
    
    Set<Id> reqIds = new Set<Id>();
    for (Return_Request__c rr : Trigger.new) {
        reqIds.add(rr.Id);
    }

   
    Map<Id, Return_Request__c> oldReqs = new Map<Id, Return_Request__c>(
        [SELECT Id, Status__c FROM Return_Request__c WHERE Id IN :reqIds]
    );

    
    for (Return_Request__c rr : Trigger.new) {
        if (String.isBlank(rr.Status__c)) {
            rr.Status__c = 'Pending';   
        }
    }
}
