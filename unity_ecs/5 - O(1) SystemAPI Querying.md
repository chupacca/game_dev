To make the code excerpt form the `ECS FEEL Example` and the `Another ECS FEEL Example` O(1), you would need to change the way you are querying the entities that have the `JumpData` component. Instead of using the `SystemAPI.Query<JumpData>` method, you could use the `Entities.WithAll<JumpData>()` method to retrieve a filtered view of all the entities that have the `JumpData` component.

**Note that the `for loop` afterwords is not O(1)**

```C#
using Unity.Entities;
using Unity.Transforms;
using Unity.Collections;

// JumpData class is a component data that implements the IComponentData interface
// it has a public field Value which is an instance of the MMFeedbacks class
public class JumpData: IComponentData
{
    public MMFeedbacks Value;
}

public class JumpSystem: SystemBase
{
    private ComponentGroup jumpDataGroup;
    protected override void OnCreateManager()
    {
        // Create a group of all entities that have the JumpData component
        jumpDataGroup = GetComponentGroup(typeof(JumpData));
    }
    protected override void OnUpdate()
    {
        if(Input.KeyDown(KeyCode.Space))
        {
            // Get the array of all entities that have the JumpData component 
            var jumpDataArray = jumpDataGroup.GetComponentDataArray<JumpData>();
            for (int i = 0; i < jumpDataArray.Length; i++)
            {
                var jumpData = jumpDataArray[i];
                jumpData.Value.PlayFeedbacks();
            }
        }
    }
}
```

By using this method, you are getting a filtered view of all the entities that have the `JumpData` component and storing it in a `jumpDataArray`. And then iterating over the array using a for loop. This way, you are directly accessing the entities that have the `JumpData` component and not iterating over all the entities in the scene to find the ones that have the `JumpData` component.

This way of querying the entities makes the code O(1) in terms of time complexity.

It is important to note that, this is just an example of how to make the code O(1) and this might not be the best solution for every case, it depends on the specific requirements of your project.

---

**How is ECS able to make the query O(1) when using `Entities.WithAll<JumpData>()`? Is it using a hash table?**


Yes, Unity's ECS uses a hash table to make the query O(1) when using the `Entities.WithAll<JumpData>()` method. When an entity is created, Unity's ECS stores a reference to the entity in a hash table where the key is the type of the component and the value is an array of entities that have that component.

When you use the `Entities.WithAll<JumpData>()` method to retrieve a filtered view of all the entities that have the `JumpData` component, Unity's ECS looks up the hash table using the `JumpData` type as the key and retrieves the array of entities that have the `JumpData` component.

This allows Unity's ECS to quickly retrieve the entities that have a specific component without having to iterate over all the entities in the scene, making the query O(1) in terms of time complexity.

It's important to note that this is an approximation of how Unity's ECS internally works and the actual implementation might differ.

It's also worth mentioning that this method of querying the entities only returns entities that were already created and added to the scene, it doesn't return entities that are going to be created in the future.
