### Q1. What is the difference between Serializable and Parcelable interfaces in Android?

**Answer**
Both Serializable and Parcelable interfaces are used to transfer data between components in Android. However, Parcelable is more efficient than Serializable when it comes to performance. Serializable uses reflection, which can slow down the serialization and deserialization process. On the other hand, Parcelable requires explicit implementation, but it performs better by using direct memory access.