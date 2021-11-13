# Laravel Relationships
# Many To Many Relationships
App\Models\Post::insert(['title'=>'Html','user_id'=>1]);
 $post = App\Models\Post::find(1);
 
 ### Attach tags to post
 $post->tags()->attach([2,3]);
 
### delete entries from pivot
 $post->tags()->detach([2,3]);

### create entries in pivot
attach(model object | ids array | single id integer)


### Querying with intermediate pivot table
$this->belongsToMany(Tag::class)->wherePivot('active',1);
wherePivotIn/wherePivotNotIn,wherePivotBetween

### if u have custom Pivot Model that has autoincrmeent primary key then must set
PostTag.php public $incrementing = true;'

### Rename pivot attribute from manytomany model Post->tags (tag has pivot object)
As noted previously, attributes from the intermediate table may be accessed on models 
via the pivot attribute. However, you are free to customize the name of this attribute to 
better reflect its purpose within your application.
use $this->belongsToMany(Tag::class)->as('assigned');

### Defining Custom Intermediate Table Models
#### define custom pivot model in many-to-many relationship, you may call using() when defining the relationship. used for define additional methods on the pivot model.
$this->belongsToMany(Tag::class)->using(PostAssignTags::class)
