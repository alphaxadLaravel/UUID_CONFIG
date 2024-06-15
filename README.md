# UUID Configurations

UUID Package for creating secured ids in the Database for the Users

## Require Package
```
composer require ramsey/uuid
```
## Migration Setups
```
Schema::create('event_photos', function (Blueprint $table) {
    $table->uuid('id')->primary();
    $table->uuid('event_id');
    $table->foreign('event_id')->references('id')->on('events')->onDelete('cascade');
    $table->string('photo');
    $table->timestamps();
});
```
## Model Setup
```
use HasFactory;

protected $fillable = [
    'event_id',
    'photo',
];

public $incrementing = false;
protected $keyType = 'string';
protected static function boot()
{
    parent::boot();
    static::creating(function ($model) {
        $model->id = Uuid::uuid4()->toString();
    });
}
```
