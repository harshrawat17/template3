---
title:  Matlab GUI - Digital Signal Processing 
layout: page
---

## Description

Designed a GUI in Matlab which takes input from user containing three frequencies and 
generates sinusoidal output with noise added to it then samples and filters it to give the noiseless 
output , both in time and frequency domain along with the filter response. The filter to be used is 
also specified by the user.

## Code
```
gui_Singleton = 1;
gui_State = struct('gui_Name',       mfilename, ...
                   'gui_Singleton',  gui_Singleton, ...
                   'gui_OpeningFcn', @LC_2017AAPS0219G_OpeningFcn, ...
                   'gui_OutputFcn',  @LC_2017AAPS0219G_OutputFcn, ...
                   'gui_LayoutFcn',  [] , ...
                   'gui_Callback',   []);
if nargin && ischar(varargin{1})
    gui_State.gui_Callback = str2func(varargin{1});
end

if nargout
    [varargout{1:nargout}] = gui_mainfcn(gui_State, varargin{:});
else
    gui_mainfcn(gui_State, varargin{:});
end



function LC_2017AAPS0219G_OpeningFcn(hObject, eventdata, handles, varargin)



handles.output = hObject;


guidata(hObject, handles);





function varargout = LC_2017AAPS0219G_OutputFcn(hObject, eventdata, handles) 



varargout{1} = handles.output;



function freq1_Callback(hObject, eventdata, handles)



freq1 = get(handles.freq1, 'String');
freq1 = str2num(freq1);
handles.freq1 = freq1;
guidata(hObject, handles);


function freq1_CreateFcn(hObject, eventdata, handles)


if ispc && isequal(get(hObject,'BackgroundColor'), get(0,'defaultUicontrolBackgroundColor'))
    set(hObject,'BackgroundColor','white');
end



function freq2_Callback(hObject, eventdata, handles)



freq2 = get(handles.freq2, 'String');
freq2 = str2num(freq2);
handles.freq2 = freq2;
guidata(hObject, handles);


function freq2_CreateFcn(hObject, eventdata, handles)



if ispc && isequal(get(hObject,'BackgroundColor'), get(0,'defaultUicontrolBackgroundColor'))
    set(hObject,'BackgroundColor','white');
end



function freq3_Callback(hObject, eventdata, handles)


freq3 = get(handles.freq3, 'String');
freq3 = str2num(freq3);
handles.freq3 = freq3;
guidata(hObject, handles);


function freq3_CreateFcn(hObject, eventdata, handles)



if ispc && isequal(get(hObject,'BackgroundColor'), get(0,'defaultUicontrolBackgroundColor'))
    set(hObject,'BackgroundColor','white');
end



function noisy_Callback(hObject, eventdata, handles)



Fs = 5200; % Sampling frequency
time = 0:1/Fs:(.01-1/Fs); % .01 second duration
handles.time = time
signal_1 = sin(2*pi*handles.freq1.*time);
signal_2 = sin(2*pi*handles.freq2.*time);
signal_3 = sin(2*pi*handles.freq3.*time);
noise = signal_1 + signal_2 + signal_3;
axes(handles.axes1);
handles.noise = noise
plot(handles.time,handles.noise);
axis([0 .01 -3 3]);
title('Noisy signal'); xlabel('t=nT_s'); ylabel('x[n]');


N=520; %FFT 
X = fft(noise,N);
%X2=fftshift(X);
X2=X(1:N/2)/(N/2);
df=Fs/N;
sampleIndex = 0:N/2-1; %raw index for FFT 
f=sampleIndex*df;
handles.f = f
axes(handles.axes2);
stem(handles.f,abs(X2)); %x-axis represent frequencies 
axis([0 2600 -3 3]);
title('X[f]');
xlabel('frequencies (f)'); 
ylabel('|X(f)|');



function filtered_Callback(hObject, eventdata, handles)



Fs = 5200; % Sampling frequency
time = 0:1/Fs:(.01-1/Fs); % 1 second duration
handles.time = time
signal_1 = sin(2*pi*handles.freq1.*time);
signal_2 = sin(2*pi*handles.freq2.*time);
signal_3 = sin(2*pi*handles.freq3.*time);
noise = signal_1 + signal_2 + signal_3;

N=22;
Wn = [3/13 10/13];
B = fir1(N,Wn,'stop');
y = filter(B, 1, noise);
axes(handles.axes1);
handles.y = y
plot(handles.time,handles.y);
title('Noisy signal filtered'); xlabel('t=nT_s'); ylabel('x[n]');

N=520; %FFT 
X = fft(y,N);
%X2=fftshift(X);
X2=X(1:N/2)/(N/2);
df=Fs/N;
sampleIndex = 0:N/2-1; %raw index for FFT 
f=sampleIndex*df;
axes(handles.axes2);
handles.f = f
stem(handles.f,abs(X2)); %x-axis represent frequencies 
title('X[f]');
xlabel('frequencies (f)'); 
ylabel('|X(f)|');



function response_Callback(hObject, eventdata, handles)


N=22;
Wn = [3/13 10/13];
B = fir1(N,Wn,'stop');
axes(handles.axes1);
stem(B)
title('filter time domain'); xlabel('t=nT_s'); ylabel('x[n]');

[H,w] = freqz(B,1,5200);
mag = 20*log10(abs(H));

axes(handles.axes2);
plot(2600*w/pi,mag);
axis ([0 2600 -100 0]);
title('filter response'); xlabel('t=nT_s'); ylabel('x[n]');
```