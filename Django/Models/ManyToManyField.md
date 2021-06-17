# ManyToManyField

- ManyToManyField creates an invisible "through" model that relates the source model to the target model.

- From the Django docs: An implicit through model class you can use to directly access the table created to hold the association. It has three fields to link the models. If the source and target models differ, the following fields are generated:

  - **id:** the primary key of the relation.
  - **<containing_model>_id:** the id of the model that declares the ManyToManyField.
  - **<other_model>_id:** the id of the model that the ManyToManyField points to.

- The invisible **"through"** model that Django uses to make **many-to-many** relationships work requires the primary keys for the source model and the target model. 
- A primary key doesn't exist until a model instance is saved, so that's why both instances have to exist before they can be related. 

### Resources
> Read more here - [Tips for Using Django's ManyToManyField](https://www.revsys.com/tidbits/tips-using-djangos-manytomanyfield/)

---
