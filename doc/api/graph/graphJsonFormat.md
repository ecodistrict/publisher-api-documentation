# Graph JSON format

This is a specification of the JSON format generic for all graphs.

#### Properties

| Property | Type | Description |
|---|---|---|
| id | string | Unique identifier of the graph. |
| apiVersion | string | Vesion of the graph format. Current version is `graph/1.0` |
| title | string | Graph title. |
| type | string | Graph type. See the possible options [here](#graphTypes). |
| axes | [Axes](#axes) | Describes what axes are used and what are their properties and settings. Each axis can have a flexible configuration, e.g. axis scale, ticks and units. Every data point is bind to one of the `x` and one of the `y` axes. |
| series | Array&lt;[Series](#series)&gt; | A list of objects to be drawn on the graph. Series type and data structure depends on a graph type. |
| clickable | `"labels"` or `undefined` | Indicates what regions of graph are clickable. This means that if client clicks on the region then a corresponding message must be sent to a backend server so that backend can react on this. **Note** that this field is temporary and will be replaced with a different one in the future. |

#### Graph types <a name="graphTypes"></a>

| Type | Description |
|---|---|
| [category](./categoryGraphJsonFormat.md) | A graph with categories on `x` axis. These graphs can contain bars and lines. |

#### Axes <a name="axes"></a>

| Property | Type | Description |
|---|---|---|
| yLeft | [Axis](#axis) | `y` axis shown on the left side of the graph. Note that at least one of the `y` axes should be specified. |
| yRight | [Axis](#axis) | `y` axis shown on the right side of the graph. Note that at least one of the `y` axes should be specified. |
| xBottom | [Axis](#axis) | `x` axis shown on the bottom of the graph. Note that at least one of the `x` axes should be specified. |
| xTop | [Axis](#axis) | `x` axis shown on the top of the graph. Note that at least one of the `x` axes should be specified. |

**Note** that each axis property name is axis id that is referenced from within data points, i.e. `"yLeft"` is the id of left `y` axis.

#### Axis <a name="axis"></a>

| Property | Type | Description |
|---|---|---|
| title | string | **Optional**. Axis title. |
| scale | Array&lt;number&gt; | **Optional**. Axis scale as an array of two elements where the first element is the axis start value and the second one is it's end. E.g. `[0, 100]` scale will result in a axis with values in the range between 0 and 100. If this property is not set then scale will be selected automatically depending on graph type and series data points. |
| formatSpecifier |	string | Ticks and tooltips numeric values formatting. Refer [d3-format](https://github.com/d3/d3-format#locale_format). |
| units | string | **Optional**. Axis units. If set then units will be displayed on the axis and together with data point value. |
| ticks | number or Array&lt;number&gt; | **Optional**. If a number then determines how many ticks will be displayed on the axis. If an array then specifies the exact ticks that should be shown, e.g. `[0, 56, 89, 100]` will display 4 ticks on the axis: 0, 56, 89 and 100.  |

#### Series <a name="series"></a>

| Property | Type | Description |
|---|---|---|
| id | string | Series id. This id will be used to identify the series so that it can be changed individually instead of changing the whole graph. Because each series is shown as a separate item in the legend the id is used to identify the series that allows enabling or disabling a certain series. |
| type | string | Series type. Possible types are defined individually for every graph type. |
| color | string | **Optional**. If defined series will have the specified color. If not defined then color will be assigned automatically. |
| title | string | Series title. Will be displayed in the legend as well as in tooltip when series is hovered. |
| data | any | Data points of the series. This property is defined individually for every graph type. |
