# The sequence of events in a Blue-Green update:

1. Begin with the existing version:
   
   - We start with a fully working version of an application, called "Version 1".

2. User initiates an update:
   
   - The user decides to update the application to a new version by making changes to its design or functionality.

3. Create the new version:
   - A new version of the application, called "Version 2", is created but kept inactive for now.

4. Preview the new version:
   - A special area, called the "Preview Service," is set up to show the new version to some users for testing purposes. The existing version, Version 1, remains active and continues to serve most users.

5. Prepare the new version for promotion:
   - The new version, Version 2, is gradually scaled up, making it available to more users through the Preview Service.
   - Meanwhile, a thorough analysis of the new version's performance, called "prePromotionAnalysis," takes place to ensure it works well.

6. Pause before promoting:
   - If necessary, the update process can be paused temporarily to give more time for testing and making any required adjustments. This helps ensure a smooth transition to the new version.
   - Once the testing period is over or a specific time has passed (as determined by "autoPromotionSeconds"), the update process automatically continues.

7. Promote the new version:
   - The new version, Version 2, is now ready to be shown to all users. The Preview Service is updated to direct traffic to Version 2.
   - At this point, there are no services pointing to the old version, Version 1.

8. Confirm the success of the update:
   - An analysis of the new version's performance, called "postPromotionAnalysis," takes place to ensure everything is working correctly.
   - Once the analysis is successful, it means the update was a success, and the new version, Version 2, is considered stable and fully promoted.

9. Scale down the old version:
   - After a specified time (usually 30 seconds, but it can be adjusted), the old version, Version 1, is scaled down and eventually removed completely. All users are now directed to the new version, Version 2.

By following these steps, we can update an application smoothly without causing any disruptions to its users.


-----------------------------------------------------------------------------

[Next](./Configurable-Features.md)