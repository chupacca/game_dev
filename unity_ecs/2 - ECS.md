```C#
using Unity.Entities;
using Unity.Transforms;
using UnityEngine;

public class ECSExample : MonoBehaviour
{
    private void Start()
    {
        // Create an entity manager
        var entityManager = World.Active.GetOrCreateManager<EntityManager>();

        // Create an entity with a position component
        var entity = entityManager.CreateEntity();
        entityManager.AddComponentData(entity, new Position { Value = Vector3.zero });

        // Update the position component every frame
        void Update()
        {
            var position = entityManager.GetComponentData<Position>(entity);
            position.Value += Vector3.right * Time.deltaTime;
            entityManager.SetComponentData(entity, position);
        }
    }
}
```

