## react-native-calendar-picker

A date picker component. You can select a range of days between two dates from the calendar modal.

### Usage

> This component use `moment.js` to process date.

**install from npm**

``` shell
npm install --save react-native-calendar-select
```

**import in project**

``` js
import Calendar from 'react-native-calendar-picker';
```

```js
constructor (props) {
  super(props);
  this.state = {
    startDate: new Date(2020, 1, 27),  
    endDate: new Date(2020, 2, 14)
  };
  this.confirmDate = this.confirmDate.bind(this);
  this.openCalendar = this.openCalendar.bind(this);
}
// When confirm button is tapped, an object is sent to outer component
// containings this properties:
// startDate [Date Object], endDate [Date Object]
// startMoment [Moment Object], endMoment [Moment Object]
confirmDate({startDate, endDate, startMoment, endMoment}) {
  this.setState({
    startDate,
    endDate
  });
}

openCalendar() {
  this.calendar && this.calendar.open();
}

render() {
  // Optional property: use it to show the structure of custom I18n object.
  let customI18n = {
    'w': ['', 'Mon', 'Tues', 'Wed', 'Thur', 'Fri', 'Sat', 'Sun'],
    'weekday': ['', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday'],
    'text': {
      'start': 'Check in',
      'end': 'Check out',
      'date': 'Date',
      'save': 'Confirm',
      'clear': 'Reset'
    },
    'date': 'DD / MM'  // Date format
  };
  // Optional
  let color = {
    subColor: '#f0f0f0'
  };
  return (
    <View>
      <Button title="Open Calendar" onPress={this.openCalendar}>
      <Calendar
        i18n="en"
        ref={(calendar) => {this.calendar = calendar;}}
        customI18n={customI18n}
        color={color}
        format="YYYYMMDD"
        minDate="20170510"
        maxDate="20180312"
        startDate={this.state.startDate}
        endDate={this.state.endDate}
        onConfirm={this.confirmDate}
      />
    </View>
  );
}
```

### Properties

| Property | Type | Default | Description |
| --- | --- | --- | --- |
| i18n | String | 'en' | Language of the component, supports `en`. |
| customI18n | Object | {} | Customize text of the component, the structure of this object is shown in the example above. |
| color | Object | {} | Customize color. |
| format | string | 'YYYY-MM-DD' | Define date format, you can also pass Date Object or Moment Object as props. |
| minDate | String / Object | - | Min date of calendar |
| maxDate | String / Object | - | Max date of calendar |
| startDate | String / Object | null | Start date of selection |
| endDate | String / Object | null | End date of selection |
| onConfirm | Function | - | Callback function when the period is confirmed, receives an object as only parameter, contains `startDate` / `endDate` / `startMoment` / `endMoment` properties. |

### Instance methods

| Method | Description |
| --- | --- |
| cancel | Cancel modification of state and close modal |
| close | Close select modal |
| open | Open select modal |
| clear | Reset state of component |
| confirm | Confirm selection and close modal |

LICENSE MIT