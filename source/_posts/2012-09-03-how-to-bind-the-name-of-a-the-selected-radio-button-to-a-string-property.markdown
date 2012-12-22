---
comments: false
date: 2012-09-03 16:41:00
layout: post
slug: how-to-bind-the-name-of-a-the-selected-radio-button-to-a-string-property
title: How to bind the name of a the selected radio button to a string property
wordpress_id: 166
categories:
- exocortex
tags:
- C#
- databinding
- wpf
---

There are three radio buttons:
- Unknown
- True
- False

The ViewModel has a string property for the name of the selected button.

The radio buttons should reflect the current value of the property and vice versa: two way binding.

Simple? F&*K no.

The XAML for the control:

[xml]

<UserControl x:Class="CustomControls.DecisionPicker"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
             xmlns:local="clr-namespace:CustomControls" mc:Ignorable="d"
    d:DesignHeight="300" d:DesignWidth="400" >
    <UserControl.Resources>
        <local:RadioButtonBoolToDecisionString x:Key="RadioButtonBoolToDecisionString"/>
    </UserControl.Resources>
        <StackPanel  x:Name="DecisionRadioButtonControl"  >
        <RadioButton GroupName="g1" IsChecked="{Binding Path=DummyDecision, Mode=TwoWay, Converter={StaticResource RadioButtonBoolToDecisionString}, ConverterParameter=Unknown}"  x:Name="UnknownRadioButton" Content="Unknown" ClickMode="Press" />
        <RadioButton GroupName="g1" IsChecked="{Binding Path=DummyDecision, Mode=TwoWay, Converter={StaticResource RadioButtonBoolToDecisionString}, ConverterParameter=True}" x:Name="TrueRadioButton" Content="True" />
        <RadioButton GroupName="g1" IsChecked="{Binding Path=DummyDecision, Mode=TwoWay, Converter={StaticResource RadioButtonBoolToDecisionString}, ConverterParameter=False}" x:Name="FalseRadioButton" Content="False" />
        </StackPanel>
</UserControl>

[/xml]

Note:



	
  * New up the value converter as a static resource in the XAML


  * The DataContext of the control is instantiated ViewModel.  The is for the MainPage.  But the control inherits it.


  * The Path of the binding is the string property on the instantiated ViewModel.






The value converter:

[csharp]
public class RadioButtonBoolToDecisionString : IValueConverter
    {
        // Convert method is from the ViewModel -> the IsChecked boolean property of the radio button
        public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
        {
            var parameterString = (string)parameter;
            string decisionString = System.Convert.ToString(value);

            if (parameterString == decisionString)
                return true;

            return false;
        }

        // ConvertBack is from the IsChecked property of the radio button to the string property on the ViewModel
        public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
        {
            var decisionStringFromControl = (string) parameter;
            return decisionStringFromControl;

        }
    }

[/csharp]

The ViewModel and MainPage setup:

[csharp]

 public partial class MainPage : UserControl
    {
        public MainPage()
        {
            InitializeComponent();

            var dvm = new DummyViewModel();
            DataContext = dvm;
            dvm.InitDecision("False");

        }
    }

 public class DummyViewModel : INotifyPropertyChanged
    {
        private string _dummyDecision;

        public string DummyDecision { get { return _dummyDecision; }
        set
        {
                _dummyDecision = value;

        }}

        public void InitDecision(string decision)
        {
            _dummyDecision = decision;
            OnPropertyChanged("DummyDecision");
        }

        public event PropertyChangedEventHandler PropertyChanged;

        protected virtual void OnPropertyChanged(string propertyName)
        {
            PropertyChangedEventHandler handler = PropertyChanged;
            if (handler != null) handler(this, new PropertyChangedEventArgs(propertyName));
        }
    }
[/csharp]
