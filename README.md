<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

use App\Models\Portfolio;

class PortfolioController extends Controller
{
    public function renderCreatePage(){
        $portfolioJobs = Portfolio::all();

        return view('createJobForPortfolio')->with('portfolioJobs', $portfolioJobs);
    }

    public function createJobForPortfolio(Request $request){
        $data = $request->all();

        $portfolioJob = Portfolio::create($data);

        return back();
    }

    public function deleteJob ($id)
    {
        $portfolioJob = Portfolio::find($id);
        if($portfolioJob) {
            $portfolioJob->delete();
        }
        return back();
    }
}
  21 changes: 18 additions & 3 deletions21  
app/Http/Controllers/SkillController.php
Original file line number	Diff line number	Diff line change
@@ -9,10 +9,25 @@
class SkillController extends Controller
{
    public function renderCreatePage(){
        return view('createSkill');
        $skills = Skill::all();

        return view('createSkill')->with('skills', $skills);
    }

    public function createSkill(Request $request){
        $data = $request->all();

        $skill = Skill::create($data);

        return back();
    }

    public function createSkill(){

    public function deleteSkill ($id)
    {
        $skill = Skill::find($id);
        if($skill) {
            $skill->delete();
        }
        return back();
    }
}
 31 changes: 31 additions & 0 deletions31  
resources/views/components/portfolioJob.blade.php
Original file line number	Diff line number	Diff line change
@@ -0,0 +1,31 @@
<div class="p-6 lg:p-8 bg-white dark:bg-gray-800 dark:bg-gradient-to-bl dark:from-gray-700/50 dark:via-transparent border-b border-gray-200 dark:border-gray-700">

    <h1 class="text-2xl font-medium text-gray-900 dark:text-white">
        Portfolios jobs
    </h1>

    <p class="mt-6 text-gray-500 dark:text-gray-400 leading-relaxed">
        Страница всех работ в портфолио
    </p>

    <div>
        <form action="" method="post">
            @csrf
            <input type="text" name="name" placeholder="Введите название работы" />

            <input type="number" min="0" name="price" />

            <input type="text" name="category" placeholder="Введите валюту" />

            <button type="submit" class="inline-flex items-center px-4 py-2 bg-gray-800 dark:bg-gray-200 border border-transparent rounded-md font-semibold text-xs text-white dark:text-gray-800 uppercase tracking-widest hover:bg-gray-700 dark:hover:bg-white focus:bg-gray-700 dark:focus:bg-white active:bg-gray-900 dark:active:bg-gray-300 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 dark:focus:ring-offset-gray-800 disabled:opacity-50 transition ease-in-out duration-150">Создать</button>
        </form>
    </div>

    @if($portfolioJobs)
        <p class="mt-6 text-gray-500 dark:text-gray-400 leading-relaxed">
            @foreach($portfolioJobs as $portfolioJob)
                {{ $portfolioJob->name }} <a href="{{ route('deleteJob', $portfolioJob->id) }}" style="color:red;">X</a><br/> 
            @endforeach
        </p>
    @endif
</div>
  94 changes: 15 additions & 79 deletions94  
resources/views/components/skills.blade.php
Original file line number	Diff line number	Diff line change
@@ -5,91 +5,27 @@
    </h1>

    <p class="mt-6 text-gray-500 dark:text-gray-400 leading-relaxed">
        Laravel Jetstream provides a beautiful, robust starting point for your next Laravel application. Laravel is designed
        to help you build your application using a development environment that is simple, powerful, and enjoyable. We believe
        you should love expressing your creativity through programming, so we have spent time carefully crafting the Laravel
        ecosystem to be a breath of fresh air. We hope you love it.
        Страница всех скиллов и их создания
    </p>
</div>

<div class="bg-gray-200 dark:bg-gray-800 bg-opacity-25 grid grid-cols-1 md:grid-cols-2 gap-6 lg:gap-8 p-6 lg:p-8">
    <div>
        <div class="flex items-center">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" class="size-6 stroke-gray-400">
                <path stroke-linecap="round" stroke-linejoin="round" d="M12 6.042A8.967 8.967 0 006 3.75c-1.052 0-2.062.18-3 .512v14.25A8.987 8.987 0 016 18c2.305 0 4.408.867 6 2.292m0-14.25a8.966 8.966 0 016-2.292c1.052 0 2.062.18 3 .512v14.25A8.987 8.987 0 0018 18a8.967 8.967 0 00-6 2.292m0-14.25v14.25" />
            </svg>
            <h2 class="ms-3 text-xl font-semibold text-gray-900 dark:text-white">
                <a href="https://laravel.com/docs">Documentation</a>
            </h2>
        </div>
        <form action="{{ route('skillCreate.post') }}" method="post">
            @csrf
            <input type="text" name="name" placeholder="Введите название скилла" />

        <p class="mt-4 text-gray-500 dark:text-gray-400 text-sm leading-relaxed">
            Laravel has wonderful documentation covering every aspect of the framework. Whether you're new to the framework or have previous experience, we recommend reading all of the documentation from beginning to end.
        </p>

        <p class="mt-4 text-sm">
            <a href="https://laravel.com/docs" class="inline-flex items-center font-semibold text-indigo-700 dark:text-indigo-300">
                Explore the documentation

                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" class="ms-1 size-5 fill-indigo-500 dark:fill-indigo-200">
                    <path fill-rule="evenodd" d="M5 10a.75.75 0 01.75-.75h6.638L10.23 7.29a.75.75 0 111.04-1.08l3.5 3.25a.75.75 0 010 1.08l-3.5 3.25a.75.75 0 11-1.04-1.08l2.158-1.96H5.75A.75.75 0 015 10z" clip-rule="evenodd" />
                </svg>
            </a>
        </p>
    </div>

    <div>
        <div class="flex items-center">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" class="size-6 stroke-gray-400">
                <path stroke-linecap="round" d="M15.75 10.5l4.72-4.72a.75.75 0 011.28.53v11.38a.75.75 0 01-1.28.53l-4.72-4.72M4.5 18.75h9a2.25 2.25 0 002.25-2.25v-9a2.25 2.25 0 00-2.25-2.25h-9A2.25 2.25 0 002.25 7.5v9a2.25 2.25 0 002.25 2.25z" />
            </svg>
            <h2 class="ms-3 text-xl font-semibold text-gray-900 dark:text-white">
                <a href="https://laracasts.com">Laracasts</a>
            </h2>
        </div>

        <p class="mt-4 text-gray-500 dark:text-gray-400 text-sm leading-relaxed">
            Laracasts offers thousands of video tutorials on Laravel, PHP, and JavaScript development. Check them out, see for yourself, and massively level up your development skills in the process.
        </p>
            <input type="number" min="0" max="100" name="lvl" />

        <p class="mt-4 text-sm">
            <a href="https://laracasts.com" class="inline-flex items-center font-semibold text-indigo-700 dark:text-indigo-300">
                Start watching Laracasts
            <input type="text" name="category" placeholder="Введите категорию" />

                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" class="ms-1 size-5 fill-indigo-500 dark:fill-indigo-200">
                    <path fill-rule="evenodd" d="M5 10a.75.75 0 01.75-.75h6.638L10.23 7.29a.75.75 0 111.04-1.08l3.5 3.25a.75.75 0 010 1.08l-3.5 3.25a.75.75 0 11-1.04-1.08l2.158-1.96H5.75A.75.75 0 015 10z" clip-rule="evenodd" />
                </svg>
            </a>
        </p>
            <button type="submit" class="inline-flex items-center px-4 py-2 bg-gray-800 dark:bg-gray-200 border border-transparent rounded-md font-semibold text-xs text-white dark:text-gray-800 uppercase tracking-widest hover:bg-gray-700 dark:hover:bg-white focus:bg-gray-700 dark:focus:bg-white active:bg-gray-900 dark:active:bg-gray-300 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 dark:focus:ring-offset-gray-800 disabled:opacity-50 transition ease-in-out duration-150">Создать скилл</button>
        </form>
    </div>

    <div>
        <div class="flex items-center">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" class="size-6 stroke-gray-400">
                <path stroke-linecap="round" stroke-linejoin="round" d="M2.25 15.75l5.159-5.159a2.25 2.25 0 013.182 0l5.159 5.159m-1.5-1.5l1.409-1.409a2.25 2.25 0 013.182 0l2.909 2.909m-18 3.75h16.5a1.5 1.5 0 001.5-1.5V6a1.5 1.5 0 00-1.5-1.5H3.75A1.5 1.5 0 002.25 6v12a1.5 1.5 0 001.5 1.5zm10.5-11.25h.008v.008h-.008V8.25zm.375 0a.375.375 0 11-.75 0 .375.375 0 01.75 0z" />
            </svg>
            <h2 class="ms-3 text-xl font-semibold text-gray-900 dark:text-white">
                <a href="https://tailwindcss.com/">Tailwind</a>
            </h2>
        </div>

        <p class="mt-4 text-gray-500 dark:text-gray-400 text-sm leading-relaxed">
            Laravel Jetstream is built with Tailwind, an amazing utility first CSS framework that doesn't get in your way. You'll be amazed how easily you can build and maintain fresh, modern designs with this wonderful framework at your fingertips.
    @if($skills)
        <p class="mt-6 text-gray-500 dark:text-gray-400 leading-relaxed">
            @foreach($skills as $skill)
                {{ $skill->name }} <a href="{{ route('skillDelete', $skill->id) }}" style="color:red;">X</a><br/> 
            @endforeach
        </p>
    </div>

    <div>
        <div class="flex items-center">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" class="size-6 stroke-gray-400">
                <path stroke-linecap="round" stroke-linejoin="round" d="M16.5 10.5V6.75a4.5 4.5 0 10-9 0v3.75m-.75 11.25h10.5a2.25 2.25 0 002.25-2.25v-6.75a2.25 2.25 0 00-2.25-2.25H6.75a2.25 2.25 0 00-2.25 2.25v6.75a2.25 2.25 0 002.25 2.25z" />
            </svg>
            <h2 class="ms-3 text-xl font-semibold text-gray-900 dark:text-white">
                Authentication
            </h2>
        </div>

        <p class="mt-4 text-gray-500 dark:text-gray-400 text-sm leading-relaxed">
            Authentication and registration views are included with Laravel Jetstream, as well as support for user email verification and resetting forgotten passwords. So, you're free to get started with what matters most: building your application.
        </p>
    </div>
</div>
    @endif
</div>
 15 changes: 15 additions & 0 deletions15  
resources/views/createJobForPortfolio.blade.php
Original file line number	Diff line number	Diff line change
@@ -0,0 +1,15 @@
<x-app-layout>
    <x-slot name="header">
        <h2 class="font-semibold text-xl text-gray-800 dark:text-gray-200 leading-tight">
            {{ __('Работы в портфолио и их добавление') }}
        </h2>
    </x-slot>

    <div class="py-12">
        <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
            <div class="bg-white dark:bg-gray-800 overflow-hidden shadow-xl sm:rounded-lg">
                <x-portfolioJob :portfolioJobs="$portfolioJobs" />
            </div>
        </div>
    </div>
</x-app-layout>
  2 changes: 1 addition & 1 deletion2  
resources/views/createSkill.blade.php
Original file line number	Diff line number	Diff line change
@@ -8,7 +8,7 @@
    <div class="py-12">
        <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
            <div class="bg-white dark:bg-gray-800 overflow-hidden shadow-xl sm:rounded-lg">
                <x-skills />
                <x-skills :skills="$skills" />
            </div>
        </div>
    </div>
  4 changes: 4 additions & 0 deletions4  
resources/views/navigation-menu.blade.php
Original file line number	Diff line number	Diff line change
@@ -18,6 +18,10 @@
                    <x-nav-link href="{{ route('skillCreate') }}" :active="request()->routeIs('dashboard')">
                        {{ __('Skills') }}
                    </x-nav-link>

                    <x-nav-link href="{{ route('createJobForPortfolio') }}" :active="request()->routeIs('dashboard')">
                        {{ __('Portfolio Jobs') }}
                    </x-nav-link>
                </div>
            </div>

  15 changes: 15 additions & 0 deletions15  
routes/web.php
Original file line number	Diff line number	Diff line change
@@ -5,6 +5,7 @@
use App\Models\Portfolio;
use App\Http\Controllers\TestController;
use App\Http\Controllers\SkillController;
use App\Http\Controllers\PortfolioController;

Route::get('/', function () {
    return view('welcome');
@@ -20,6 +21,20 @@

Route::get('/create-skill', [SkillController::class, 'renderCreatePage'])->middleware('auth')->name('skillCreate');

Route::post('/create-skill', [SkillController::class, 'CreateSkill'])->middleware('auth')->name('skillCreate.post');

Route::get('/delete-skill/{id}', [SkillController::class, 'deleteSkill'])->middleware('auth')->name('skillDelete');



Route::get('/create-job-for-portfolio', [PortfolioController::class, 'renderCreatePage'])->middleware('auth')->name('createJobForPortfolio');

Route::post('/create-job-for-portfolio', [PortfolioController::class, 'createJobForPortfolio'])->middleware('auth')->name('createJobForPortfolio.post');

Route::get('/delete-portfolio-job/{id}', [PortfolioController::class, 'deleteJob'])->middleware('auth')->name('deleteJob');



Route::get('/portfolio', function(){
    $title = 'Портфолио Terricon';

