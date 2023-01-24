# How to bind Schedule commands in Xamarin.Forms (SfSchedule) 

You can bind the ViewModel commands to [CellDoubleTappedCommand](https://help.syncfusion.com/cr/xamarin/Syncfusion.SfSchedule.XForms.SfSchedule.html#Syncfusion_SfSchedule_XForms_SfSchedule_CellDoubleTappedCommand) and [VisibleDatesChangedCommand](https://help.syncfusion.com/cr/xamarin/Syncfusion.SfSchedule.XForms.SfSchedule.html#Syncfusion_SfSchedule_XForms_SfSchedule_VisibleDatesChangedCommand) of [SfSchedule](https://www.syncfusion.com/xamarin-ui-controls/xamarin-scheduler) in Xamarin.Forms.

`STEP 1:` Create a ViewModel class and define a `VisibleDatesChangedCommand` and `CellDoubleTappedCommand`.
```
public class SchedulerViewModel : INotifyPropertyChanged
{
 
        public SchedulerViewModel()
        {
            this.VisibleDatesChangedCommand = new Command<VisibleDatesChangedEventArgs>(OnVisibleDatesChanged);
            this.CellDoubleTappedCommand = new Command<CellTappedEventArgs>(OnCellDoubleTapped);
        }
 
        /// <summary>
        /// Cell Double Tapped event
        /// </summary>
        /// <param name="obj"></param>
        private void OnCellDoubleTapped(CellTappedEventArgs obj)
        {
            App.Current.MainPage.DisplayAlert("CellDoubleTapped", "Event Triggered", "ok");
        }
 
        /// <summary>
        /// Visible Dates changed Event
        /// </summary>
        /// <param name="obj"></param>
        private void OnVisibleDatesChanged(VisibleDatesChangedEventArgs obj)
        {
            App.Current.MainPage.DisplayAlert("VisibleDateChanged", "Event Triggered", "ok");
 
        }
 
        /// <summary>
        /// Visible Dates changed Command.
        /// </summary>
        public ICommand VisibleDatesChangedCommand { get; set; }
 
        /// <summary>
        /// CellDoubleTapped command.
        /// </summary>
        public ICommand CellDoubleTappedCommand { get; set; }
 
        /// <summary>
        /// Occurs when property changed.
        /// </summary>
        public event PropertyChangedEventHandler PropertyChanged;
 
        /// <summary>
        /// Invoke method when property changed.
        /// </summary>
        /// <param name="propertyName">property name</param>
        private void RaiseOnPropertyChanged(string propertyName)
        {
            this.PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
        }
}
```
`STEP 2:` Bind the VisibleDatesChangedCommand  and CellDoubleTappedCommand  of ViewModel to the CellDoubleTappedCommand and VisibleDatesChangedCommand  in SfSchedule.
```
<schedule:SfSchedule x:Name="Schedule"
                                 VisibleDatesChangedCommand="{Binding VisibleDatesChangedCommand}"
                                 CellDoubleTappedCommand="{Binding CellDoubleTappedCommand}"
                                 ScheduleView="MonthView">
            <schedule:SfSchedule.BindingContext>
                <local:SchedulerViewModel/>
            </schedule:SfSchedule.BindingContext>
</schedule:SfSchedule>
```

KB article - [How to bind Schedule commands in Xamarin.Forms (SfSchedule)](https://www.syncfusion.com/kb/11817/how-to-bind-schedule-commands-in-xamarin-forms-sfschedule)