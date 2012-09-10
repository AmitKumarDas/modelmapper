# Converters

Converters allow custom conversion to take place when mapping to a destination type or property. 

### Creating a Converter

Converters can be implemented in two ways. The first is by extending `AbstractConverter`:

```
Converter<String, String> toUppercase = new AbstractConverter<String, String>() {
  @Override
  protected String convert(String source) {
    return source == null ? null : source.toUppercase();
  }
};
```

The second way is by implementing the `Converter` interface which exposes a `MappingContext` that contains contains information related to the current mapping request:

```
Converter<String, String> toUppercase = new Converter<String, String>() {
  @Override
  public String convert(MappingContext<String, String> context) {
    return context.getSource() == null ? null : context.getSource().toUppercase();
  }
};
```

### Configuration

Converters can be configured for use in several ways. The first is by adding the converter to a ModelMapper:

```
modelMapper.addConverter(personConverter);
```

This, in turn, sets the converter against the TypeMap corresponding to the source and destination types `Person` and `PersonDTO`.

A Converter can also be set directly against a TypeMap:

```
personTypeMap.setConverter(personConverter);
```

We can also specify a Converter to be used when converting properties within a TypeMap:

```
personTypeMap.setPropertyConverter(propertyConverter);
```

Converters can also be set for specific properties. See the mapping API page on [PropertyConverters converters] for more info using converters with properties.