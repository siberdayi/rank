<?php

namespace Vendor\RankExtension;

use Flarum\Extend;
use Illuminate\Contracts\Events\Dispatcher;
use Flarum\Api\Serializer\UserSerializer;

return [
    (new Extend\Frontend('forum'))
        ->css(__DIR__ . '/../resources/less/rank.less')
        ->content(function ($content) {
            $content->setVariable('userRank', function ($user) {
                return $user->rank ?? 'Üye';
            });
        }),

    (new Extend\ApiSerializer(UserSerializer::class))
        ->attribute('rank', function ($serializer, $user) {
            return $user->rank ?? 'Üye';
        }),

    (new Extend\Event())
        ->listen(
            \Flarum\User\Event\Saving::class,
            function ($event) {
                if (isset($event->data['attributes']['rank'])) {
                    $event->user->rank = $event->data['attributes']['rank'];
                }
            }
        ),

    (new Extend\User())
        ->attribute('rank')
];  bu ne kodu

